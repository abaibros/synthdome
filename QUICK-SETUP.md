🚀 SynthDome - synthdome.com 연동 빠른 가이드
==============================================

## ⚡ 3단계 빠른 설정

### 1️⃣ GitHub Pages 활성화 (1분)
```
https://github.com/abaibros/synthdome/settings/pages
↓
Source: main 브랜치 선택
↓ 
Save 클릭
```

### 2️⃣ 커스텀 도메인 입력 (30초)
```
같은 페이지에서
↓
Custom domain: synthdome.com 입력
↓
Save 클릭
```

### 3️⃣ DNS 설정 (5분)

도메인 업체(GoDaddy, Cloudflare 등)에서:

**A 레코드 4개 추가:**
```
Type: A
Name: @
Value: 185.199.108.153
Value: 185.199.109.153
Value: 185.199.110.153
Value: 185.199.111.153
```

**CNAME 레코드 1개 추가:**
```
Type: CNAME
Name: www
Value: abaibros.github.io
```

---

## ⏱️ 대기 시간
- DNS 전파: 1-48시간 (보통 1-2시간)
- HTTPS 자동 활성화: DNS 전파 후 5-10분

---

## ✅ 완료 확인
1-2시간 후:
- https://synthdome.com 접속
- 동영상 배경 홈페이지 확인

---

## 🔗 지금 바로 확인 (GitHub Pages URL)
```
https://abaibros.github.io/synthdome/
```
↑ DNS 설정 전에도 이 URL로 바로 접속 가능!

---

## 📞 문의
- 전화: +82)10-8496-1440 / +82)10-4224-2020
- 이메일: synthdome.ceo@gmail.com

상세 가이드: GITHUB-PAGES-SETUP.md 참조
