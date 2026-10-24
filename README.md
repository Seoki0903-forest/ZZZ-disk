# ZZZ 디스크 판정 데이터

Android 앱이 실행될 때 이 저장소의 data/manifest.json을 확인하고, SHA-256이 바뀐 캐릭터 파일만 다운로드합니다. APK 업데이트와 독립적으로 배포됩니다.

- data/manifest.json: 데이터 버전, 캐릭터 경로와 SHA-256, 미완성 캐릭터 목록
- data/characters/*.json: 캐릭터별 4세트·2세트·주옵션·유효/필수 부옵션과 출시 순서
- schemaVersion: 1

모든 파일을 준비한 뒤 manifest와 함께 한 커밋으로 게시합니다. 캐릭터를 수정하면 해당 SHA-256과 manifest의 전체 version도 다시 계산해야 합니다. version은 version 필드를 제외한 manifest를 키 정렬·공백 없는 UTF-8 JSON과 마지막 줄바꿈으로 직렬화한 SHA-256입니다.

클라이언트는 HTTPS와 파일 해시·데이터 형식을 검사하고 전체 검증 후 한 번에 적용합니다. 실패하면 마지막 정상 데이터를 유지합니다.
