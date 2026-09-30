## What it does

`ask-matt`는 이 plugin에서 삭제되었다. 이 페이지는 기존 링크를 위한 삭제 안내이며, 실행 가능한 skill이나 새 router를 제공하지 않는다.

skill 선택과 흐름 routing은 consuming harness가 소유한다. 이 plugin의 고정 skill 목록을 전체 설치 목록으로 간주하지 않는다.

## When to reach for it

이 plugin에서 `/ask-matt`를 호출하지 않는다. 사용할 skill과 흐름은 consuming harness의 routing 안내와 프로젝트 지침을 확인한다.

## Common questions

**`ask-matt` 소스가 빠진 것인가?**

아니다. [삭제 commit](https://github.com/dongwoo-labs/mattpocock-skills/commit/f8026d8b28658f20daed65b8c4d4d015d63fc034)이 source와 plugin whitelist 항목을 의도적으로 제거했다. 이 문서 때문에 삭제된 `SKILL.md`를 복원하거나 필수 dependency로 취급하지 않는다.

**다른 harness의 router도 사용할 수 없는가?**

이 plugin의 삭제만 설명한다. consuming harness의 router 제공 여부, 이름, 호출 방법은 해당 harness의 계약을 따른다. 이 문서는 alias나 fallback을 지정하지 않는다.

## It's working if

- 이 plugin의 문서가 삭제된 `/ask-matt` 호출이나 소스 재동기화를 요구하지 않는다.
- skill 선택은 consuming harness의 지침을 따르고, 개별 skill의 역할은 해당 source에서 확인한다.

## Where it fits

이 plugin은 개별 skill을 제공하고, consuming harness는 선택과 routing을 소유한다. 이 삭제 안내는 routing이나 작업 실행 권한을 대신하지 않는다.
