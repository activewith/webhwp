# 웹 한글 편집기 (webhwp)

브라우저에서 HWP·HWPX 문서를 열고 편집·저장하는 웹앱(PWA)입니다.
주소: https://hwp.activewith.net

- 편집 엔진·UI: [rhwp](https://github.com/edwardkim/rhwp) v0.8.7 (MIT, Edward Kim) 정적 빌드
- 문서는 브라우저 안에서만 처리되며 서버로 전송되지 않습니다.
- 휴대폰: 주소 접속 후 브라우저 메뉴의 "홈 화면에 추가"(iOS Safari는 공유 → 홈 화면에 추가)로 앱처럼 설치. 설치 후 오프라인에서도 동작합니다.

## 알려진 제한
- 한컴 전용 글꼴이 없어 화면 모양이 한컴오피스와 다를 수 있습니다.
- HWP(바이너리)로 다시 저장하면 손상될 수 있습니다. 중요한 문서는 HWPX 저장을 권장합니다.
- 휴대폰 브라우저에서는 같은 파일에 덮어쓰기가 되지 않고 다운로드 폴더에 새 파일로 저장됩니다.
- 입찰·적격심사 제출 서류는 한컴오피스에서 최종 확인 후 제출하십시오.

## 배포 구성
- GitHub Pages: main 브랜치 / 루트 폴더
- `CNAME`: hwp.activewith.net (DNS: `hwp` CNAME → `activewith.github.io`)
- `.nojekyll`: Jekyll 처리 생략

## 업데이트 방법 (rhwp 새 버전 반영)
```bash
git clone https://github.com/edwardkim/rhwp.git && cd rhwp && git checkout v<버전>
npm pack @rhwp/core@<버전> && tar xzf rhwp-core-<버전>.tgz
mkdir -p pkg && cp package/rhwp* pkg/ && cp pkg/rhwp.js pkg/rhwp_bg.wasm rhwp-studio/public/
cd rhwp-studio && npm ci
RHWP_WITHOUT_HWPCTRL=1 npx vite build --base ./ --outDir dist-rel
```
빌드 후 `dist-rel` 내용으로 이 저장소 파일을 교체하고, `manifest.webmanifest`의
`start_url`·`scope`·`file_handlers[].action`을 `./`로 수정한 뒤 `CNAME`·`.nojekyll`·`README.md`를 유지해 커밋합니다.

## 라이선스
- rhwp: MIT — `LICENSE-rhwp.txt`
- 글꼴: `fonts/FONTS.md`
