# MeD2 - 한글을 지원하는 Meslo

![GitHub release (latest by date)](https://img.shields.io/github/v/release/partrita/MeD2?style=flat-square)
![License](https://img.shields.io/github/license/partrita/MeD2?style=flat-square)
![Build Status](https://img.shields.io/github/actions/workflow/status/partrita/MeD2/release-font.yml?style=flat-square)

**MeD2**는 Meslo와 D2Coding의 뛰어난 한글 지원을 결합한 프로그래밍 글꼴입니다. 이 글꼴은 영문과 한글 텍스트가 모두 포함된 코드에 최적의 가독성을 제공합니다.

## ✨ 특징

- **완벽한 한글 지원**: D2Coding의 한글 글리프(U+3131-U+318E, U+AC00-U+D7A3)를 포함합니다.
- **다양한 버전**: 일반 글꼴, 아이콘이 포함된 Nerd Font 버전, 웹 폰트를 제공합니다.
- **최적화된 간격**: 가독성 향상을 위해 문자 너비를 세심하게 조정했습니다.
- **크로스플랫폼**: Windows, macOS, Linux에서 작동합니다.

## 📥 다운로드

[Releases](https://github.com/partrita/MeD2/releases) 페이지에서 최신 글꼴을 다운로드하세요.

### 설치

#### Windows
1. `.ttf` 파일 다운로드
2. 마우스 오른쪽 버튼을 클릭하고 "설치" 또는 "모든 사용자용으로 설치" 선택
3. 애플리케이션 다시 시작

#### macOS
1. `.ttf` 파일 다운로드
2. 더블 클릭하여 서체 관리자 열기
3. "서체 설치" 클릭
4. 애플리케이션 다시 시작

#### Linux
1. `.ttf` 파일 다운로드
2. `~/.local/share/fonts/` 또는 `/usr/share/fonts/`로 복사
3. `fc-cache -fv` 실행
4. 애플리케이션 다시 시작

## 🛠️ 소스에서 빌드하기

### 사전 요구사항

빌드하기 전에 다음이 필요합니다:
- Python 3.7+
- FontForge (Python 바인딩 포함)
- wget 및 unzip 유틸리티

### 방법 1: Nix 사용 (권장)

모든 종속성을 관리하며 MeD2를 빌드하는 가장 쉬운 방법입니다:

```bash
# 저장소 복제
git clone https://github.com/partrita/MeD2.git
cd MeD2

# Nix 개발 환경 진입
nix develop

# 글꼴 빌드 (에셋 자동 다운로드)
python scripts/build.py build

# 완료 후 종료
exit
```

### 방법 2: Docker 사용

컨테이너화된 환경에서 빌드합니다:

```bash
# Docker 이미지 복제 및 빌드
git clone https://github.com/partrita/MeD2.git
cd MeD2
docker build -t fontbuild .

# 대화형 컨테이너 실행
docker run -it -v "$(pwd)":/app fontbuild

# 컨테이너 내부: 글꼴 빌드
python3 scripts/build.py build

# 컨테이너 종료
exit
```

### 방법 3: 수동 설정

종속성을 수동으로 설정하려는 고급 사용자를 위한 방법입니다:

#### Ubuntu/Debian
```bash
sudo apt-get update
sudo apt-get install fontforge python3-fontforge wget unzip
```

#### macOS
```bash
brew install fontforge wget
pip3 install fontforge-python
```

#### 수동 빌드 과정
```bash
# 저장소 복제
git clone https://github.com/partrita/MeD2.git
cd MeD2

# 글꼴 빌드
python3 scripts/build.py build

# 정리 (선택 사항)
python3 scripts/build.py clean
```

### 빌드 명령어

| 명령어 | 설명 |
|---------|-------------|
| `python scripts/build.py build` | 기존 에셋으로 글꼴 빌드 |
| `python scripts/build.py test` | 글꼴 빌드 과정 테스트 |
| `python scripts/build.py clean` | 생성된 파일 정리 |

## 🎨 사용 예시

### VS Code
`settings.json`에 다음을 추가하세요:
```json
{
    "editor.fontFamily": "MeD2, Consolas, monospace",
    "editor.fontLigatures": true,
    "editor.fontSize": 14
}
```

### 터미널 (Nerd Font 버전 사용 시)
```bash
# 글꼴 설치 확인
fc-list | grep MeD2

# 터미널이 MeD2NerdFont-Regular를 사용하도록 설정
```

### 웹 프로젝트
```css
@font-face {
    font-family: 'MeD2';
    src: url('path/to/MeD2-Regular.woff2') format('woff2');
    font-display: swap;
}

code, pre {
    font-family: 'MeD2', 'Fira Code', monospace;
}
```

## ⚙️ 설정

`scripts/config.py` 파일에 빌드 설정 옵션이 있습니다:

- `KOREAN_FONT_WIDTH`: 한글 문자 너비
- `ENGLISH_FONT_WIDTH`: 영문 문자 너비
- `TARGET_EM`: 글꼴 스케일링을 위한 Target em 크기
- 글꼴 소스 경로 및 출력 디렉토리

## 🤝 기여하기

1. 저장소 Fork
2. 기능 브랜치 생성: `git checkout -b feature/amazing-feature`
3. 변경사항 적용
4. 빌드 과정 테스트
5. 변경사항 커밋: `git commit -m 'Add amazing feature'`
6. 브랜치에 푸시: `git push origin feature/amazing-feature`
7. Pull Request 생성

## 📋 요구사항

### 소스 글꼴
- **Meslo**: 합자를 포함한 기본 프로그래밍 글꼴
- **D2Coding**: 한글 지원을 위한 한국어 코딩 글꼴
- **Meslo Nerd Font**: 아이콘이 추가된 버전

### 빌드 종속성
- Python 3.7+
- FontForge (Python 바인딩 포함)
- 기본 Unix 유틸리티 (wget, unzip)

## 🐛 알려진 문제

- 일부 터미널 에뮬레이터에서 합자가 올바르게 표시되지 않을 수 있습니다.
- 웹 폰트 로딩 시 적절한 CORS 헤더가 필요할 수 있습니다.
- 특정 애플리케이션에서는 글꼴 메트릭 조정이 필요할 수 있습니다.
- [x] The glyph named Omega is mapped to U+03A9. But its name indicates it should be mapped to U+2126.
    - U+03A9 글리프의 이름을 'uni03A9'로 변경하여 FontForge 경고를 우회합니다.
- The following table(s) in the font have been ignored by FontForge
    - Ignoring 'LTSH' linear threshold table
    - Ignoring 'VDMX' vertical device metrics table
    - Ignoring 'hdmx' horizontal device metrics table

## 📄 라이선스

이 프로젝트는 [SIL Open Font License 1.1](LICENSE)에 따라 라이선스가 부여됩니다.

### 글꼴 라이선스
- **Meslo**: SIL OFL 1.1
- **D2Coding**: SIL OFL 1.1
- **Nerd Fonts**: MIT License

## 🙏 감사


- [D2Coding](https://github.com/naver/d2codingfont) - NAVER
- [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts) 프로젝트

---

**한글과 영문 코드를 다루는 개발자들을 위해 ❤️ 로 만들었습니다**
