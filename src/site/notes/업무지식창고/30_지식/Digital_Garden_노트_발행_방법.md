---
{"dg-publish":true,"dg-permalink":"ellie-hyun/digital-garden","permalink":"/ellie-hyun/digital-garden/","title":"Digital Garden 노트 발행 방법","tags":["Digital Garden","Obsidian","발행","공유"],"dg-note-properties":{"title":"Digital Garden 노트 발행 방법","date":"2026-06-30","tags":["Digital Garden","Obsidian","발행","공유"],"type":"지식","related":[]}}
---


# Digital Garden 노트 발행 방법

Obsidian 노트를 외부에 공유할 수 있는 웹사이트로 발행하는 방법.

---



## 🆕 처음 발행하는 노트

**① 공개할 노트 열기**

**② `Ctrl + P` → `publish` 입력 → "Add publish flag" 클릭**
→ 프론트매터에 `dg-publish: true` 자동 추가됨

**③ `Ctrl + P` → "Publish Active Note" 클릭**

**④ 1~2분 후 사이트맵에서 URL 확인**
```
https://grand-rabanadas-f1205a.netlify.app/sitemap.xml
```
→ 발행된 노트의 정확한 URL 목록 확인 가능

---

## ✏️ 이미 발행한 노트 수정 후

**① 노트 수정**

**② `Ctrl + P` → "Publish Active Note" 클릭**

**③ 1~2분 후 링크에 자동 반영**

> 수정 시 재발행 필수! 자동 반영 안 됨.

---

## 🔗 내 사이트 주소

```
https://grand-rabanadas-f1205a.netlify.app
```

---

## ⚠️ 주의사항

| 상황           | 해결 방법                                                    |
| ------------ | -------------------------------------------------------- |
| URL 모를 때     | `sitemap.xml` 에서 확인                                      |
| 발행 취소하고 싶을 때 | `Ctrl+P` → "Remove publish flag" → "Publish Active Note" |
| 여러 노트 한번에 발행 | `Ctrl+P` → "Publish All Notes Marked for Publish"        |

---

## 🔗 URL 미리 지정하기 (dg-permalink)

발행 전에 **내가 원하는 URL을 직접 지정**할 수 있음. 이렇게 하면 sitemap 확인 없이 URL을 미리 알 수 있다.

**프론트매터에 추가:**

```yaml
dg-permalink: my-note
```

**결과 URL:** `https://grand-rabanadas-f1205a.netlify.app/my-note`

> 💡 한글보다 영문 슬러그 추천 (URL이 짧고 깔끔해짐)

---

## ⚡ Templater로 URL 자동 복사하기

단축키 하나로 현재 노트의 발행 URL을 클립보드에 자동 복사.

### 1단계 — 스크립트 파일 만들기

`90_자료/` 폴더에 `URL복사.md` 파일을 만들고 아래 내용 저장:

~~~
<%*
const BASE_URL = "https://grand-rabanadas-f1205a.netlify.app";
const file = app.workspace.getActiveFile();
const fm = app.metadataCache.getFileCache(file)?.frontmatter;

let url;
if (fm?.['dg-permalink']) {
  url = `${BASE_URL}/${fm['dg-permalink'].replace(/^\//, '')}`;
} else {
  const slug = file.basename.toLowerCase().replace(/[\s_]+/g, '-');
  url = `${BASE_URL}/notes/${slug}`;
}

await navigator.clipboard.writeText(url);
new Notice(`📋 복사됨!\n${url}`, 5000);
%>
~~~

### 2단계 — 단축키 지정

1. `설정 → Templater → Template Hotkeys`
2. `+` 버튼 클릭
3. `URL복사.md` 선택 → 원하는 단축키 지정 (예: `Ctrl + Shift + U`)

### 3단계 — 사용

발행된 노트에서 단축키 누르면 → URL 자동 복사 완료 ✅

---

## 📌 자주 쓰는 명령어 모음

| 명령어                                                    | 기능                    |
| ------------------------------------------------------ | --------------------- |
| `Digital Garden: Add publish flag`                     | `dg-publish: true` 추가 |
| `Digital Garden: Publish Active Note`                  | 현재 노트 발행              |
| `Digital Garden: Publish All Notes Marked for Publish` | 발행 표시된 노트 전체 발행       |
| `Digital Garden: Remove publish flag`                  | 발행 취소                 |
| `Digital Garden: Open Publication Center`              | 발행 현황 전체 확인           |
