# 비욘드 잉글리쉬 사송캠퍼스 — 안내 페이지

인스타그램 프로필이나 카카오톡에 붙일 **링크 한 개짜리 홈페이지**입니다.
링크트리 같은 서비스를 쓰지 않고 직접 띄웁니다.

**BESync(원내 운영 시스템)와는 완전히 별개입니다.** 저장소도 배포도 서로 영향을
주지 않습니다.

---

## 무엇이 들어 있나

```
index.html          페이지 전부 (HTML 한 장)
assets/
  logo.png          BE 마크
  og.png            카카오톡·인스타에 링크를 붙였을 때 보이는 미리보기 그림
  favicon.png       브라우저 탭 아이콘
  apple-touch-icon.png
tools/
  og-source.html    og.png 을 다시 만들 때 쓰는 원본 (배포와 무관)
```

빌드도 설치도 없습니다. `index.html` 하나면 동작합니다.

---

## 링크 바꾸기 — 개발 도구 없이

GitHub 웹 화면에서 바로 고칠 수 있습니다.

1. 이 저장소에서 `index.html` 을 연다
2. 오른쪽 위 **연필 아이콘**을 누른다
3. `href="#"` 안에 주소를 넣는다
4. 아래 **Commit changes** 를 누른다
5. 1~2분 뒤 실제 페이지에 반영된다

`index.html` 안에 어디를 고쳐야 하는지 주석으로 적어 두었습니다.

| 버튼 | 넣을 주소 |
|---|---|
| ~~카카오톡으로 상담 신청하기~~ | ✅ 연결됨 (주 버튼) |
| ~~카카오톡으로 빠른 상담~~ | ✅ 연결됨 |
| 비욘드 교육과정 살펴보기 | 블로그 글 주소 |
| 사송캠퍼스 수업 이야기 | 블로그 글 주소 |
| 전화로 문의하기 | `tel:055-000-0000` |
| ~~학원 위치 · 주차 안내~~ | ✅ 네이버 지도 검색으로 연결됨 |
| ~~인스타그램 · 네이버 블로그~~ | ✅ 연결됨 |

맨 아래 등록번호는 **양산교육지원청 등록 제2285호** 로 넣어 두었습니다.
학원 광고에는 등록번호 표기가 법으로 요구되므로, 틀렸다면 바로 고쳐야 합니다.

### 쓰지 않을 버튼은 지운다

블로그가 없다면 «교육과정»·«수업 이야기» 줄은 통째로 지우는 편이 낫습니다.
눌러도 아무 일이 없는 버튼은 없느니만 못합니다.

---

## 어디에 배포하나

**Cloudflare Pages** 를 씁니다. 무료이고, **무료 요금제에서 상업적 사용을
명시적으로 허용**하며, 대역폭 제한이 없고 서울에 서버가 있어 빠릅니다.

> **Vercel 은 쓰면 안 됩니다.** Hobby 요금제는 «비상업적 개인 사용» 으로
> 제한되고, 약관이 «상품·서비스의 판매를 광고하는 것» 을 상업적 사용의 예로
> 명시합니다. 학원 홍보 페이지가 정확히 여기에 해당합니다.
> — https://vercel.com/docs/limits/fair-use-guidelines
>
> GitHub Pages 도 «온라인 비즈니스 운영» 을 금지하고 있어 회색지대입니다.

### 처음 한 번

1. https://dash.cloudflare.com 에서 학원 계정으로 가입 (무료, 카드 불필요)
2. **Workers & Pages → Create application → Pages 탭 → Connect to Git**
   (기본이 Workers 탭이라 Pages 로 옮겨야 한다)
3. 이 저장소를 고른다
4. 빌드 설정 — **아무것도 넣지 않는다**
   - Framework preset: `None`
   - Build command: *(비움)*
   - Build output directory: `/`
5. **Save and Deploy**

배포 주소는 **https://beyond-sasong.pages.dev** 입니다.

### 주소가 바뀌면 두 줄을 함께 고친다

도메인을 붙이는 등 주소가 바뀌면 `index.html` 위쪽의 이 두 줄도 같이 바꿔야
카카오톡 미리보기 카드가 계속 뜹니다. **카카오톡은 상대 경로를 읽지 못하고
전체 주소를 요구합니다.**

```html
<meta property="og:url" content="https://beyond-sasong.pages.dev/">
<meta property="og:image" content="https://beyond-sasong.pages.dev/assets/og.png">
```

이미 카카오톡으로 링크를 보낸 적이 있다면
[카카오 디버거](https://developers.kakao.com/tool/clear/og)에서 캐시를 지워야
새 이미지가 보입니다. 카카오는 한 번 읽은 미리보기를 한동안 쥐고 있습니다.

### 그다음부터

`main` 에 push 하면 자동으로 다시 배포됩니다. 따로 할 일이 없습니다.

---

## 도메인 (권장)

인스타그램 프로필에 `xxx.pages.dev` 를 적는 것보다 학원 이름 도메인이 낫습니다.
연 1.5만원 안팎이고 월 고정비는 없습니다.

1. 도메인을 산다 (Cloudflare Registrar 는 원가에 팝니다 · `.kr` 은 가비아·후이즈)
2. Cloudflare Pages → **Custom domains → Set up a domain**
3. 안내대로 DNS 를 넣으면 인증서까지 자동으로 붙습니다

도메인을 바꿔도 이 저장소는 그대로입니다.

---

## 미리보기 그림 다시 만들기

문구나 로고가 바뀌면 `assets/og.png` 도 새로 만들어야 카카오톡 미리보기가
맞습니다.

1. `tools/og-source.html` 을 고친다
2. 브라우저에서 **1200 × 630** 크기로 열어 화면을 캡처한다
3. `assets/og.png` 를 덮어쓴다

---

## 로컬에서 확인

```bash
npx serve .
```

http://localhost:3000 에서 열립니다. 그냥 `index.html` 을 브라우저로 열어도
대부분 동작하지만, 미리보기 태그까지 제대로 보려면 위 방법이 낫습니다.
