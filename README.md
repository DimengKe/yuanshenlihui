[Uploading index.html…]()
<!DOCTYPE html>
<html lang="zh-cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>原神角色立绘展示</title>
    <style>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f0f0f0;
}

header {
    position: relative;
    width: 100%;
    height: 300px;
    overflow: hidden;
}

.carousel-container {
    position: relative;
    width: 100%;
    height: 100%;
}

.carousel {
    position: relative;
    width: 100%;
    height: 100%;
}

.slide {
    position: absolute;
    top: 0;
    height: 100%;
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center;
    transition: background-size 0.5s ease, background-position 0.5s ease, transform 0.5s ease, opacity 0.5s ease;
}

.left {
    left: 0;
    width: 100%;
    background-size: contain;
    background-position: center;
    z-index: 1;
    transform: translateX(-10%) rotate(-2deg);
    opacity: 0.8;
}

.middle {
    left: 0;
    width: 100%;
    background-size: contain;
    background-position: center;
    z-index: 3;
    transform: none;
    opacity: 1;
}

.right {
    left: 0;
    width: 100%;
    background-size: contain;
    background-position: center;
    z-index: 2;
    transform: translateX(10%) rotate(2deg);
    opacity: 0.8;
}

.carousel-btn {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background-color: rgba(0, 0, 0, 0.5);
    color: white;
    border: none;
    padding: 10px;
    cursor: pointer;
    font-size: 18px;
    z-index: 10;
}

.carousel-btn:hover {
    background-color: rgba(0, 0, 0, 0.8);
}

.prev {
    left: 10px;
}

.next {
    right: 10px;
}

nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    background-color: #fff;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.elements {
    display: flex;
    gap: 10px;
}

.element-btn {
    background: none;
    border: none;
    cursor: pointer;
    padding: 5px;
}

.element-btn img {
    width: 50px;
    height: 50px;
}

.filters {
    display: flex;
    gap: 10px;
}

.filter-btn {
    padding: 10px 20px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.filter-btn:hover {
    background-color: #0056b3;
}

main {
    padding: 20px;
}

.character-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 20px;
    max-width: 1200px;
    margin: 0 auto;
}

@media (max-width: 768px) {
    .character-grid {
        grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
    }
}

.character-card {
    background-color: white;
    border-radius: 4px;
    overflow: hidden;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    cursor: pointer;
    transition: transform 0.2s;
}

.character-card:hover {
    transform: scale(1.05);
}

.character-card img {
    width: 100%;
    height: 100px;
    object-fit: contain;
    background-color: #f0f0f0;
}

.character-info {
    padding: 0px;
    text-align: center;
}

.character-name {
    font-weight: bold;
    font-size: 12px;
    margin-bottom: 3px;
}

.character-rarity {
    font-size: 10px;
    color: #ffd700;
}

.four-star {
    color: #c0c0c0;
}

.modal {
    display: none;
    position: fixed;
    z-index: 10;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(0,0,0,0.4);
}

.modal-content {
    background-color: #fefefe;
    margin: 5% auto;
    padding: 20px;
    border: 1px solid #888;
    width: auto;
    max-width: 90vw;
    max-height: 90vh;
    border-radius: 10px;
    overflow: auto;
}

.close {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
    cursor: pointer;
}

.close:hover {
    color: black;
}

.images {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
}

.image-item {
    text-align: center;
}

.image-item p {
    margin: 0 0 5px 0;
    font-size: 14px;
    font-weight: bold;
    color: #333;
}

.images img {
    width: auto;
    height: auto;
}
    </style>
</head>
<body>
    <header>
        <div class="carousel-container">
            <div class="carousel">
                <div class="slide left"></div>
                <div class="slide middle"></div>
                <div class="slide right"></div>
            </div>
            <button id="prevBtn" class="carousel-btn prev">&lt;</button>
            <button id="nextBtn" class="carousel-btn next">&gt;</button>
        </div>
    </header>
    <nav>
        <div class="elements">
            <button class="element-btn" data-element="wind">🌪️</button>
            <button class="element-btn" data-element="fire">🔥</button>
            <button class="element-btn" data-element="thunder">⚡️</button>
            <button class="element-btn" data-element="water">💧</button>
            <button class="element-btn" data-element="ice">❄️</button>
            <button class="element-btn" data-element="rock">🪨</button>
            <button class="element-btn" data-element="grass">🌱</button>
        </div>
        <div class="filters">
            <button class="filter-btn" data-filter="all">全部角色</button>
            <button class="filter-btn" data-filter="fiveStar">五星角色</button>
            <button class="filter-btn" data-filter="fourStar">四星角色</button>
        </div>
    </nav>
    <main>
        <div id="character-grid" class="character-grid">
            <!-- 角色头像将在这里动态生成 -->
        </div>
    </main>
    <div id="character-modal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 id="modal-name"></h2>
            <div class="images">
                <div class="image-item">
                    <p>横版立绘</p>
                    <img id="portrait-h" src="" alt="横版立绘">
                </div>
                <div class="image-item">
                    <p>竖版立绘</p>
                    <img id="portrait-v" src="" alt="竖版立绘">
                </div>
                <div class="image-item">
                    <p>抽卡立绘</p>
                    <img id="gacha" src="" alt="抽卡立绘">
                </div>
                <div class="image-item">
                    <p>生日立绘</p>
                    <img id="birthday" src="" alt="生日立绘">
                </div>
                <div class="image-item">
                    <p>角色名片</p>
                    <img id="namecard" src="" alt="角色名片">
                </div>
                <div class="image-item" id="wallpaper-item" style="display: none;">
                    <p>活动壁纸</p>
                    <img id="wallpaper" src="" alt="活动壁纸">
                </div>
            </div>
        </div>
    </div>
    <script>
// 角色数据定义 - 修改此部分可添加新角色或更改现有角色的图片信息
const characterData = {
    // 风元素角色列表 - 添加新风元素角色在此数组中
    wind: [
        {
            name: "温迪", // 角色名称
            rarity: 5, // 星级：5为五星，4为四星
            avatar: "https://upload-bbs.mihoyo.com/upload/2020/11/25/f85355d6b04bf7161378d7123e2a0bd4.jpeg?x-oss-process=image/resize,s_150/quality,q_80/auto-orient,0/interlace,1/format,jpg",
            images: { // 立绘图片对象
                portraitH: "https://via.placeholder.com/400x300/87CEEB/FFFFFF?text=温迪+横版立绘", // 横版立绘
                portraitV: "https://via.placeholder.com/300x400/87CEEB/FFFFFF?text=温迪+竖版立绘", // 竖版立绘
                gacha: "https://via.placeholder.com/400x500/87CEEB/FFFFFF?text=温迪+抽卡立绘", // 抽卡立绘
                birthday: "https://via.placeholder.com/400x300/87CEEB/FFFFFF?text=温迪+生日立绘", // 生日立绘
                namecard: "https://via.placeholder.com/300x400/87CEEB/FFFFFF?text=温迪+角色名片", // 角色名片
                wallpaper: "https://via.placeholder.com/800x600/87CEEB/FFFFFF?text=温迪+活动壁纸" // 活动壁纸（五星角色专用）
            }
        }
        // 在此添加更多风元素角色，使用相同格式
    ],
    // 火元素角色列表 - 添加新火元素角色在此数组中
    fire: [
        {
            name: "迪卢克",
            rarity: 5,
            avatar: "https://via.placeholder.com/150x200/FF6B35/FFFFFF?text=迪卢克+头像",
            images: {
                portraitH: "https://via.placeholder.com/400x300/FF6B35/FFFFFF?text=迪卢克+横版立绘",
                portraitV: "https://via.placeholder.com/300x400/FF6B35/FFFFFF?text=迪卢克+竖版立绘",
                gacha: "https://via.placeholder.com/400x500/FF6B35/FFFFFF?text=迪卢克+抽卡立绘",
                birthday: "https://via.placeholder.com/400x300/FF6B35/FFFFFF?text=迪卢克+生日立绘",
                namecard: "https://via.placeholder.com/300x400/FF6B35/FFFFFF?text=迪卢克+角色名片",
                wallpaper: "https://via.placeholder.com/800x600/FF6B35/FFFFFF?text=迪卢克+活动壁纸"
            }
        },
        {
            name: "香菱",
            rarity: 4, // 四星角色没有wallpaper字段
            avatar: "https://via.placeholder.com/150x200/FF6B35/FFFFFF?text=香菱+头像",
            images: {
                portraitH: "https://via.placeholder.com/400x300/FF6B35/FFFFFF?text=香菱+横版立绘",
                portraitV: "https://via.placeholder.com/300x400/FF6B35/FFFFFF?text=香菱+竖版立绘",
                gacha: "https://via.placeholder.com/400x500/FF6B35/FFFFFF?text=香菱+抽卡立绘",
                birthday: "https://via.placeholder.com/400x300/FF6B35/FFFFFF?text=香菱+生日立绘",
                namecard: "https://via.placeholder.com/300x400/FF6B35/FFFFFF?text=香菱+角色名片"
                // 注意：四星角色不包含wallpaper
            }
        }
        // 在此添加更多火元素角色
    ],
    // 雷元素角色列表
    thunder: [
        {
            name: "雷电将军",
            rarity: 5,
            avatar: "https://via.placeholder.com/150x200/FFD700/FFFFFF?text=雷电将军+头像",
            images: {
                portraitH: "https://via.placeholder.com/400x300/FFD700/FFFFFF?text=雷电将军+横版立绘",
                portraitV: "https://via.placeholder.com/300x400/FFD700/FFFFFF?text=雷电将军+竖版立绘",
                gacha: "https://via.placeholder.com/400x500/FFD700/FFFFFF?text=雷电将军+抽卡立绘",
                birthday: "https://via.placeholder.com/400x300/FFD700/FFFFFF?text=雷电将军+生日立绘",
                namecard: "https://via.placeholder.com/300x400/FFD700/FFFFFF?text=雷电将军+角色名片",
                wallpaper: "https://via.placeholder.com/800x600/FFD700/FFFFFF?text=雷电将军+活动壁纸"
            }
        },
        {
            name: "瓦雷莎",
            rarity: 5,
            avatar: "https://bbs-static.miyoushe.com/static/2025/02/25/d7797c4b6dddc28b349127fac553be9f_8091135422383674950.png?x-oss-process=image/resize,s_150/quality,q_80/auto-orient,0/interlace,1/format,jpg",
            images: {
                portraitH: "https://upload-bbs.miyoushe.com/upload/2025/03/10/364887579/362a2cc4745c26273b03533b2fcc3cea_250136657388825679.jpg?x-oss-process=image//resize,s_600/quality,q_80/auto-orient,0/interlace,1/format,jpg",
                portraitV: "https://upload-bbs.miyoushe.com/upload/2025/03/10/364887579/034219560ad943d56ba0a9dae6b98a99_1932849408926565958.jpg?x-oss-process=image//resize,s_600/quality,q_80/auto-orient,0/interlace,1/format,jpg",
                gacha: "https://upload-bbs.miyoushe.com/upload/2025/04/12/364887579/7ab3c3afea7414ae8053713e4bb9f06e_6703074204645824085.webp?x-oss-process=image//resize,s_600/quality,q_80/auto-orient,0/interlace,1/format,webp",
                birthday: "https://via.placeholder.com/400x300/FFD700/FFFFFF?text=瓦雷莎+生日立绘",
                namecard: "https://upload-bbs.miyoushe.com/upload/2025/04/12/364887579/04067cc1f9a63b4b16f9150a51b70a4e_8049040482846815266.webp?x-oss-process=image//resize,s_600/quality,q_80/auto-orient,0/interlace,1/format,webp",
                wallpaper: "https://via.placeholder.com/800x600/FFD700/FFFFFF?text=瓦雷莎+活动壁纸"
            }
        }
    ],
    // 水元素角色列表
    water: [
        {
            name: "莫娜",
            rarity: 5,
            avatar: "https://via.placeholder.com/150x200/1E88E5/FFFFFF?text=莫娜+头像",
            images: {
                portraitH: "https://via.placeholder.com/400x300/1E88E5/FFFFFF?text=莫娜+横版立绘",
                portraitV: "https://via.placeholder.com/300x400/1E88E5/FFFFFF?text=莫娜+竖版立绘",
                gacha: "https://via.placeholder.com/400x500/1E88E5/FFFFFF?text=莫娜+抽卡立绘",
                birthday: "https://via.placeholder.com/400x300/1E88E5/FFFFFF?text=莫娜+生日立绘",
                namecard: "https://via.placeholder.com/300x400/1E88E5/FFFFFF?text=莫娜+角色名片",
                wallpaper: "https://via.placeholder.com/800x600/1E88E5/FFFFFF?text=莫娜+活动壁纸"
            }
        }
    ],
    // 冰元素角色列表
    ice: [
        {
            name: "甘雨",
            rarity: 5,
            avatar: "https://via.placeholder.com/150x200/4FC3F7/FFFFFF?text=甘雨+头像",
            images: {
                portraitH: "https://via.placeholder.com/400x300/4FC3F7/FFFFFF?text=甘雨+横版立绘",
                portraitV: "https://via.placeholder.com/300x400/4FC3F7/FFFFFF?text=甘雨+竖版立绘",
                gacha: "https://via.placeholder.com/400x500/4FC3F7/FFFFFF?text=甘雨+抽卡立绘",
                birthday: "https://via.placeholder.com/400x300/4FC3F7/FFFFFF?text=甘雨+生日立绘",
                namecard: "https://via.placeholder.com/300x400/4FC3F7/FFFFFF?text=甘雨+角色名片",
                wallpaper: "https://via.placeholder.com/800x600/4FC3F7/FFFFFF?text=甘雨+活动壁纸"
            }
        }
    ],
    // 岩元素角色列表
    rock: [
        {
            name: "希诺宁",
            rarity: 5,
            avatar: "https://bbs-static.miyoushe.com/static/2024/08/28/95ae86a1aea16edb032d3ba462200d7d_8064454282205880152.png?x-oss-process=image/resize,s_150/quality,q_80/auto-orient,0/interlace,1/format,jpg",
            images: {
                portraitH: "https://via.placeholder.com/400x300/8D6E63/FFFFFF?text=希诺宁+横版立绘",
                portraitV: "https://via.placeholder.com/300x400/8D6E63/FFFFFF?text=希诺宁+竖版立绘",
                gacha: "https://via.placeholder.com/400x500/8D6E63/FFFFFF?text=希诺宁+抽卡立绘",
                birthday: "https://via.placeholder.com/400x300/8D6E63/FFFFFF?text=希诺宁+生日立绘",
                namecard: "https://via.placeholder.com/300x400/8D6E63/FFFFFF?text=希诺宁+角色名片",
                wallpaper: "https://via.placeholder.com/800x600/8D6E63/FFFFFF?text=希诺宁+活动壁纸"
            }
        }
    ],
    // 草元素角色列表
    grass: [
        {
            name: "纳西妲",
            rarity: 5,
            avatar: "https://via.placeholder.com/150x200/4CAF50/FFFFFF?text=纳西妲+头像",
            images: {
                portraitH: "https://via.placeholder.com/400x300/4CAF50/FFFFFF?text=纳西妲+横版立绘",
                portraitV: "https://via.placeholder.com/300x400/4CAF50/FFFFFF?text=纳西妲+竖版立绘",
                gacha: "https://via.placeholder.com/400x500/4CAF50/FFFFFF?text=纳西妲+抽卡立绘",
                birthday: "https://via.placeholder.com/400x300/4CAF50/FFFFFF?text=纳西妲+生日立绘",
                namecard: "https://via.placeholder.com/300x400/4CAF50/FFFFFF?text=纳西妲+角色名片",
                wallpaper: "https://via.placeholder.com/800x600/4CAF50/FFFFFF?text=纳西妲+活动壁纸"
            }
        }
    ]
    // 如需添加新元素，在此添加新属性，如 dendro: [...]
};

// 自动生成列表 - 无需修改，此部分根据characterData自动生成
const allCharacters = []; // 全部角色列表
const fiveStarCharacters = []; // 五星角色列表
const fourStarCharacters = []; // 四星角色列表

Object.values(characterData).forEach(elementChars => {
    elementChars.forEach(char => {
        allCharacters.push(char);
        if (char.rarity === 5) {
            fiveStarCharacters.push(char);
        } else if (char.rarity === 4) {
            fourStarCharacters.push(char);
        }
    });
});

// 页面交互逻辑 - 无需修改，除非需要改变交互行为
document.addEventListener('DOMContentLoaded', () => {
    // 轮播图逻辑
    let currentSlide = 0;
    const imageUrls = [
        "https://bbs-static.miyoushe.com/static/2026/01/08/9dd8c49e2ba06b2eb009adfa28c76b3e_6371517207002793753.png",
        "https://bbs-static.miyoushe.com/static/2026/01/07/ab4c0fec14a1d6c010b0ea2f1f369916_5540768489676651557.jpg",
        "https://bbs-static.miyoushe.com/static/2026/01/02/7388d8856bda27dec4e89a3085cb2a5a_8649693396816231448.png",
    ];
    const slides = document.querySelectorAll('.slide');
    const carousel = document.querySelector('.carousel');
    const prevBtn = document.getElementById('prevBtn');
    const nextBtn = document.getElementById('nextBtn');
    let intervalId;

    function showSlide(index) {
        currentSlide = index;
        if (currentSlide >= imageUrls.length) currentSlide = 0;
        if (currentSlide < 0) currentSlide = imageUrls.length - 1;
        let prevIndex = (currentSlide - 1 + imageUrls.length) % imageUrls.length;
        let nextIndex = (currentSlide + 1) % imageUrls.length;
        slides[0].style.backgroundImage = `url(${imageUrls[prevIndex]})`; // left
        slides[1].style.backgroundImage = `url(${imageUrls[currentSlide]})`; // middle
        slides[2].style.backgroundImage = `url(${imageUrls[nextIndex]})`; // right
    }

    function nextSlide() {
        showSlide(currentSlide + 1);
    }

    function prevSlide() {
        showSlide(currentSlide - 1);
    }

    function startSlideshow() {
        intervalId = setInterval(nextSlide, 5000); // 5秒切换
    }

    function stopSlideshow() {
        clearInterval(intervalId);
    }

    // 鼠标悬停暂停
    carousel.addEventListener('mouseenter', stopSlideshow);
    carousel.addEventListener('mouseleave', startSlideshow);

    // 按钮事件
    prevBtn.addEventListener('click', prevSlide);
    nextBtn.addEventListener('click', nextSlide);

    // 初始化轮播
    showSlide(0);
    startSlideshow();
    const characterGrid = document.getElementById('character-grid');
    const modal = document.getElementById('character-modal');
    const modalName = document.getElementById('modal-name');
    const portraitH = document.getElementById('portrait-h');
    const portraitV = document.getElementById('portrait-v');
    const gacha = document.getElementById('gacha');
    const birthday = document.getElementById('birthday');
    const namecard = document.getElementById('namecard');
    const wallpaper = document.getElementById('wallpaper');
    const closeBtn = document.querySelector('.close');

    let currentCharacters = allCharacters;

    // 显示角色网格
    function displayCharacters(characters) {
        characterGrid.innerHTML = '';
        characters.forEach(char => {
            const card = document.createElement('div');
            card.className = 'character-card';
            card.innerHTML = `
                <img src="${char.avatar}" alt="${char.name}">
                <div class="character-info">
                    <div class="character-name">${char.name}</div>
                    <div class="character-rarity ${char.rarity === 5 ? 'five-star' : 'four-star'}">${'★'.repeat(char.rarity)}</div>
                </div>
            `;
            card.addEventListener('click', () => showModal(char));
            characterGrid.appendChild(card);
        });
    }

    // 显示模态框
    function showModal(char) {
        modalName.textContent = char.name;
        portraitH.src = char.images.portraitH;
        portraitV.src = char.images.portraitV;
        gacha.src = char.images.gacha;
        birthday.src = char.images.birthday;
        namecard.src = char.images.namecard;
        const wallpaperItem = document.getElementById('wallpaper-item');
        if (char.rarity === 5) {
            wallpaper.src = char.images.wallpaper;
            wallpaperItem.style.display = 'block';
        } else {
            wallpaperItem.style.display = 'none';
        }
        modal.style.display = 'block';
    }

    // 关闭模态框
    closeBtn.addEventListener('click', () => {
        modal.style.display = 'none';
    });

    window.addEventListener('click', (event) => {
        if (event.target === modal) {
            modal.style.display = 'none';
        }
    });

    // 元素按钮事件
    document.querySelectorAll('.element-btn').forEach(btn => {
        btn.addEventListener('click', () => {
            const element = btn.dataset.element;
            currentCharacters = characterData[element] || [];
            displayCharacters(currentCharacters);
        });
    });

    // 过滤按钮事件
    document.querySelectorAll('.filter-btn').forEach(btn => {
        btn.addEventListener('click', () => {
            const filter = btn.dataset.filter;
            if (filter === 'all') {
                currentCharacters = allCharacters;
            } else if (filter === 'fiveStar') {
                currentCharacters = fiveStarCharacters;
            } else if (filter === 'fourStar') {
                currentCharacters = fourStarCharacters;
            }
            displayCharacters(currentCharacters);
        });
    });

    // 初始显示全部角色
    displayCharacters(allCharacters);
});
    </script>
</body>
</html>
