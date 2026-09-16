<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MBTI로 내 포켓몬 찾기</title>
    <style>
        body {
            background-color: #FFF9E6; /* 따뜻한 크림색 */
            color: #333;
            font-family: 'Malgun Gothic', 'Apple SD Gothic Neo', sans-serif;
            text-align: center;
            margin: 0;
            padding: 20px;
        }
        h1 {
            font-size: 2.5rem;
            color: #D4A017;
        }
        p {
            font-size: 1.2rem;
            line-height: 1.6;
        }
        #mbti-container {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px;
            max-width: 600px;
            margin: 30px auto;
        }
        @media (max-width: 500px) {
            #mbti-container {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        .mbti-btn {
            background-color: #FFEAA7; /* 노란색 톤 */
            border: 2px solid #FDCB6E;
            border-radius: 10px;
            padding: 20px 10px;
            font-size: 1.5rem;
            font-weight: bold;
            color: #555;
            cursor: pointer;
            transition: 0.2s;
        }
        .mbti-btn:hover {
            background-color: #FDCB6E;
            color: #000;
        }
        #result-screen {
            display: none;
            max-width: 600px;
            margin: 0 auto;
            background-color: #FFFFFF;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        #pokemon-image {
            width: 250px;
            height: 250px;
            object-fit: contain;
            margin: 20px 0;
        }
        #pokemon-name {
            font-size: 2.5rem;
            font-weight: bold;
            color: #E17055;
            margin-bottom: 10px;
        }
        .desc-box {
            background-color: #FFF9E6;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
        }
        .match-box {
            font-size: 1.3rem;
            font-weight: bold;
            color: #0984E3;
            margin-bottom: 30px;
        }
        .reset-btn {
            background-color: #FDCB6E;
            border: none;
            border-radius: 10px;
            padding: 15px 30px;
            font-size: 1.5rem;
            font-weight: bold;
            cursor: pointer;
        }
        .reset-btn:hover {
            background-color: #E1B12C;
        }
    </style>
</head>
<body>

    <div id="main-screen">
        <h1>MBTI로 내 포켓몬 찾기</h1>
        <p>당신의 MBTI를 선택해 보세요.</p>
        <div id="mbti-container">
            <!-- 자바스크립트로 버튼 생성됨 -->
        </div>
    </div>

    <div id="result-screen">
        <h2>당신과 어울리는 포켓몬은...</h2>
        <img id="pokemon-image" src="" alt="포켓몬 이미지">
        <div id="pokemon-name"></div>
        
        <div class="desc-box">
            <p id="pokemon-desc"></p>
        </div>

        <div class="match-box">
            최고의 찰떡 궁합: <span id="best-match"></span>
        </div>

        <button class="reset-btn" onclick="reset()">다시 고르기</button>
    </div>

    <script>
        const pokemonData = {
            "ISTJ": { name: "꼬부기", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/7.png", desc: "주어진 일을 묵묵히 해내는 책임감이 강합니다.<br>항상 원칙을 지키며 주변 사람들에게 깊은 신뢰를 줍니다.", match: "ESFP (피카츄)" },
            "ISFJ": { name: "이상해씨", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png", desc: "온화하고 헌신적이며 타인을 돕는 것을 좋아합니다.<br>조용하지만 단단한 내면을 가지고 있어 무리에서 큰 의지가 됩니다.", match: "ESTP (꼬마돌)" },
            "INFJ": { name: "라프라스", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/131.png", desc: "통찰력이 뛰어나고 신비로운 분위기를 풍깁니다.<br>사람들의 감정을 깊이 이해하고 따뜻하게 품어주는 능력이 있습니다.", match: "ENTP (팬텀)" },
            "INTJ": { name: "뮤츠", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/150.png", desc: "고도로 독립적이고 전략적인 사고를 합니다.<br>냉철한 판단력으로 목표를 향해 흔들림 없이 나아갑니다.", match: "ENFP (토게피)" },
            "ISTP": { name: "스라크", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/123.png", desc: "상황 판단이 빠르고 논리적이며 과묵합니다.<br>위기 상황에서도 당황하지 않고 문제를 해결하는 능력이 뛰어납니다.", match: "ESFJ (럭키)" },
            "ISFP": { name: "식스테일", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/37.png", desc: "예술적 감각이 뛰어나고 온화한 성격을 가졌습니다.<br>다투는 것을 싫어하며 현재의 순간을 즐길 줄 아는 여유가 있습니다.", match: "ESTJ (니드킹)" },
            "INFP": { name: "메타몽", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/132.png", desc: "상상력이 풍부하고 유연하며 이상주의자입니다.<br>어떤 환경이나 사람에게도 잘 맞춰줄 수 있는 넓은 수용력이 있습니다.", match: "ENFJ (망나뇽)" },
            "INTP": { name: "잠만보", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/143.png", desc: "느긋해 보이지만 머릿속은 분석과 생각으로 가득합니다.<br>관심 있는 분야에는 놀라운 집중력을 보여줍니다.", match: "ENTJ (리자몽)" },
            "ESTP": { name: "꼬마돌", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/74.png", desc: "현실적이고 활동적이며 어디서든 적응을 잘합니다.<br>거침없는 행동력으로 주변에 활력을 불어넣습니다.", match: "ISFJ (이상해씨)" },
            "ESFP": { name: "피카츄", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png", desc: "어디서나 주목받는 분위기 메이커입니다.<br>넘치는 에너지와 사교성으로 사람들을 즐겁게 만듭니다.", match: "ISTJ (꼬부기)" },
            "ENFP": { name: "토게피", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/175.png", desc: "긍정적이고 열정적이며 호기심이 아주 많습니다.<br>새로운 가능성을 찾아다니며 주변에 해피 바이러스를 전파합니다.", match: "INTJ (뮤츠)" },
            "ENTP": { name: "팬텀", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/94.png", desc: "독창적이고 장난기가 많으며 고정관념을 깹니다.<br>재치 있는 입담과 번뜩이는 아이디어로 늘 신선한 충격을 줍니다.", match: "INFJ (라프라스)" },
            "ESTJ": { name: "니드킹", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/34.png", desc: "체계적이고 리더십이 있으며 매우 현실적입니다.<br>강한 추진력으로 무리를 이끌고 목표를 확실하게 달성합니다.", match: "ISFP (식스테일)" },
            "ESFJ": { name: "럭키", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/113.png", desc: "타고난 다정함으로 주변 사람들을 살뜰히 챙깁니다.<br>타인의 감정에 공감하고 협력하는 것을 가장 중요하게 생각합니다.", match: "ISTP (스라크)" },
            "ENFJ": { name: "망나뇽", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/149.png", desc: "카리스마 있고 이타적이며 타고난 언변가입니다.<br>사람들의 성장을 돕고 긍정적인 영향을 미치는 것을 즐깁니다.", match: "INFP (메타몽)" },
            "ENTJ": { name: "리자몽", image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/6.png", desc: "결단력이 뛰어나고 거침없이 목표를 향해 돌진합니다.<br>강력한 리더십으로 닥친 문제들을 논리적이고 확실하게 타파합니다.", match: "INTP (잠만보)" }
        };

        const mbtiList = ["ISTJ", "ISFJ", "INFJ", "INTJ", "ISTP", "ISFP", "INFP", "INTP", "ESTP", "ESFP", "ENFP", "ENTP", "ESTJ", "ESFJ", "ENFJ", "ENTJ"];
        
        const container = document.getElementById("mbti-container");
        const mainScreen = document.getElementById("main-screen");
        const resultScreen = document.getElementById("result-screen");

        // 버튼 생성
        mbtiList.forEach(mbti => {
            const btn = document.createElement("button");
            btn.className = "mbti-btn";
            btn.innerText = mbti;
            btn.onclick = () => showResult(mbti);
            container.appendChild(btn);
        });

        function showResult(mbti) {
            const data = pokemonData[mbti];
            document.getElementById("pokemon-image").src = data.image;
            document.getElementById("pokemon-name").innerText = data.name + " (" + mbti + ")";
            document.getElementById("pokemon-desc").innerHTML = data.desc;
            document.getElementById("best-match").innerText = data.match;

            mainScreen.style.display = "none";
            resultScreen.style.display = "block";
        }

        function reset() {
            resultScreen.style.display = "none";
            mainScreen.style.display = "block";
        }
    </script>
</body>
</html>
