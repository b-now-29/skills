---
name: git-guardrails-claude-code
description: 위험한 git 명령(push, reset --hard, clean, branch -D 등)이 실행되기 전에 차단하도록 Claude Code 훅을 설정합니다. 사용자가 파괴적인 git 작업을 방지하거나, git 안전 훅을 추가하거나, Claude Code에서 git push/reset을 차단하고자 할 때 사용합니다.
---

# Git 안전장치 설정

Claude가 위험한 git 명령을 실행하기 전에 이를 가로채어 차단하는 PreToolUse 훅을 설정합니다.

## 차단되는 항목

- `git push` (`--force`를 포함한 모든 변형)
- `git reset --hard`
- `git clean -f` / `git clean -fd`
- `git branch -D`
- `git checkout .` / `git restore .`

차단되면, Claude는 해당 명령에 접근할 권한이 없다는 메시지를 보게 됩니다.

## 단계

### 1. 범위 질문

사용자에게 질문하십시오. **이 프로젝트에만**(`.claude/settings.json`) 설치할 것인지, **모든 프로젝트**(`~/.claude/settings.json`)에 설치할 것인지 묻습니다.

### 2. 훅 스크립트 복사

번들된 스크립트는 다음 위치에 있습니다: [scripts/block-dangerous-git.sh](scripts/block-dangerous-git.sh)

범위에 따라 대상 위치로 복사하십시오.

- **프로젝트**: `.claude/hooks/block-dangerous-git.sh`
- **전역**: `~/.claude/hooks/block-dangerous-git.sh`

`chmod +x`로 실행 가능하게 만드십시오.

### 3. 설정에 훅 추가

적절한 설정 파일에 추가하십시오.

**프로젝트** (`.claude/settings.json`):

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/hooks/block-dangerous-git.sh"
          }
        ]
      }
    ]
  }
}
```

**전역** (`~/.claude/settings.json`):

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "~/.claude/hooks/block-dangerous-git.sh"
          }
        ]
      }
    ]
  }
}
```

설정 파일이 이미 존재하는 경우, 기존 `hooks.PreToolUse` 배열에 훅을 병합하십시오. 다른 설정을 덮어쓰지 마십시오.

### 4. 사용자 정의에 대해 질문

차단 목록에 패턴을 추가하거나 제거하고 싶은지 사용자에게 물으십시오. 그에 따라 복사된 스크립트를 편집하십시오.

### 5. 검증

빠른 테스트를 실행하십시오.

```bash
echo '{"tool_input":{"command":"git push origin main"}}' | <path-to-script>
```

종료 코드 2로 종료되고 stderr에 BLOCKED 메시지를 출력해야 합니다.
