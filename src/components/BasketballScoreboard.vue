<template>

    <div class="scoreboard">

        <div class="left-team-buttons">
            <button @click="changeScore('team1', 3)">+3</button>
            <button @click="changeScore('team1', 2)">+2</button>
            <button @click="changeScore('team1', 1)">+1</button>
        </div>
        <div class="right-team-buttons">
            <button @click="changeScore('team2', 3)">+3</button>
            <button @click="changeScore('team2', 2)">+2</button>
            <button @click="changeScore('team2', 1)">+1</button>
        </div>
        <div class="match-statistics-buttons">
            <button @click="showMatchStatistics = !showMatchStatistics">Match Statistics</button>
        </div>

        <!-- Основная табличка со счетом -->
        <div class="scoreboard__main">
            <div class="scoreboard__team scoreboard__team--left">
                <div class="scoreboard__logo-wrapper logo-wrapper logo-wrapper--left">
                    <div
                        class="scoreboard__logo-container"
                        :class="{ 'logo1--hidden': teams.team1.showScore }"
                    >
                        <img
                            src="./../assets/team1-logo.png"
                            alt="BIP Lions"
                            class="scoreboard__logo"
                        />
                    </div>
                    <div
                        class="scoreboard__score-text scoreboard__score-text--left"
                        :class="{ 'score-text--shown': teams.team1.showScore }"
                    >
                        +{{ teams.team1.score }}
                    </div>
                </div>
                <div class="scoreboard__team-name-wrapper">
                    <div class="scoreboard__team-name">BIP Lions</div>
                </div>
            </div>
            <div class="scoreboard__indicators scoreboard__indicators-left">
                <div class="scoreboard__line">
                    <span class="scoreboard__dash scoreboard__dash--active"></span>
                    <span class="scoreboard__dash scoreboard__dash--active"></span>
                    <span class="scoreboard__dash scoreboard__dash--active"></span>
                    <span class="scoreboard__dash scoreboard__dash--active"></span>
                    <span class="scoreboard__dash"></span>
                </div>
                <div class="scoreboard__bottom-row">
                    <div class="scoreboard__circles">
                        <span class="scoreboard__circle"></span>
                        <span class="scoreboard__circle scoreboard__circle--active"></span>
                        <span class="scoreboard__circle scoreboard__circle--active"></span>
                    </div>
                    <div class="scoreboard-scores">
                        <span class="scoreboard__number">20</span>
                        <span class="scoreboard__number">20</span>
                        <span class="scoreboard__number">10</span>
                        <span class="scoreboard__number scoreboard__number--active">10</span>
                    </div>
                </div>
            </div>
            <div class="scoreboard-score score">
                <div class="score-inner scoreboard-score-inner">
                    <div class="score__number-left">86</div>
                    <div class="scoreboard-score__divider">:</div>
                    <div class="score__number-right">184</div>
                </div>
            </div>
            <div class="scoreboard__indicators scoreboard__indicators-right">
                <div class="scoreboard__line">
                    <span class="scoreboard__dash scoreboard__dash--active"></span>
                    <span class="scoreboard__dash scoreboard__dash--active"></span>
                    <span class="scoreboard__dash scoreboard__dash--active"></span>
                    <span class="scoreboard__dash scoreboard__dash--active"></span>
                    <span class="scoreboard__dash scoreboard__dash--active"></span>
                </div>
                <div class="scoreboard__bottom-row">
                    <div class="scoreboard-scores">
                        <span class="scoreboard__number">20</span>
                        <span class="scoreboard__number">20</span>
                        <span class="scoreboard__number">10</span>
                        <span class="scoreboard__number scoreboard__number--active">10</span>
                    </div>
                    <div class="scoreboard__circles">
                        <span class="scoreboard__circle scoreboard__circle--active"></span>
                        <span class="scoreboard__circle"></span>
                        <span class="scoreboard__circle"></span>
                    </div>
                </div>
            </div>
            <div class="scoreboard__team scoreboard__team--right">
                <div class="scoreboard__team-name-wrapper">
                    <div class="scoreboard__team-name">Банк Уралсиб</div>
                </div>
                <div class="scoreboard__logo-wrapper logo-wrapper logo-wrapper--right">
                    <div
                        class="scoreboard__logo-container"
                        :class="{ 'logo2--hidden': teams.team2.showScore }"
                    >
                        <img
                            src="./../assets/team2-logo.png"
                            alt="BIP Lions"
                            class="scoreboard__logo"
                        />
                    </div>
                    <div
                        class="scoreboard__score-text scoreboard__score-text--right"
                        :class="{ 'score-text--shown': teams.team2.showScore }"
                    >
                        +{{ teams.team2.score }}
                    </div>
                </div>
            </div>
        </div>


        <!-- Верхняя панель с таймером и номером четверти -->
        <div class="scoreboard__overlay">
            <div class="scoreboard__quarter">1</div>
            <div class="scoreboard__divider"></div>
            <div class="scoreboard__timer">10:00</div>
        </div>

        <!-- Блоки с информацией об игроке -->
        <div class="scoreboard__player-info scoreboard__player-info--left">
            <Transition name="slide-fade">
                <div
                    v-if="teams.team1.showPhoto"
                    class="scoreboard__player-photo-wrapper"
                >
                    <img
                        src="./../assets/player1.webp"
                        alt="John Doe"
                        class="scoreboard__player-photo"
                    >
                </div>
            </Transition>
            <Transition name="slide-fade">
                <div
                    v-if="teams.team1.showStats"
                    class="scoreboard__player-info-inner scoreboard__player-info-inner-left"
                >
                    <div class="scoreboard__player-name">Андреев Сергей</div>
                    <div class="scoreboard__player-stats">
                        <div class="scoreboard__stat"><span>Очки:</span> 25</div>
                        <div class="scoreboard__stat"><span>2-очк:</span> 5/10</div>
                        <div class="scoreboard__stat"><span>3-очк:</span> 3/7</div>
                        <div class="scoreboard__stat"><span>4-очк:</span> 0/2</div>
                    </div>
                </div>
            </Transition>
        </div>
        <div class="scoreboard__player-info scoreboard__player-info--right">
            <Transition name="slide-fade">
                <div
                    v-if="teams.team2.showStats"
                    class="scoreboard__player-info-inner"
                >
                    <div class="scoreboard__player-stats">
                        <div class="scoreboard__stat"><span>Очки:</span> 18</div>
                        <div class="scoreboard__stat"><span>2-очк:</span> 4/8</div>
                        <div class="scoreboard__stat"><span>3-очк:</span> 2/5</div>
                        <div class="scoreboard__stat"><span>4-очк:</span> 1/1</div>
                    </div>
                    <div class="scoreboard__player-name">Яннис Адетокунбо</div>
                </div>
            </Transition>
            <Transition name="slide-fade">
                <div
                    v-if="teams.team2.showPhoto"
                    class="scoreboard__player-photo-wrapper"
                >
                    <img
                        src="./../assets/player1.webp"
                        alt="John Doe"
                        class="scoreboard__player-photo"
                    >
                </div>
            </Transition>
        </div>


        <!-- Статистика матча -->
        <div
            class="scoreboard__content"
            :class="{ 'scoreboard__content--hidden': !showMatchStatistics }"
        >
            <table class="scoreboard__table table">
                <caption>
                    <h3 class="table__caption">Статистика матча</h3>
                </caption>
                <thead class="table__head">
                    <tr class="table__row table__row-head">
                        <th class="table__cell table__cell-head">
                            <div class="team">
                                <div class="team__logo-wrapper logo-wrapper logo-wrapper--left">
                                    <img
                                        src="./../assets/team1-logo.png"
                                        alt="BIP Lions"
                                        class="scoreboard__logo"
                                    >
                                </div>
                                <div class="table__team-name">BIP Lions</div>
                            </div>

                        </th>

                        <th class="table__cell table__cell-head">
                            <div class="score table-score">
                                <div class="score-inner table-score-inner">
                                    <div class="score__number-left">86</div>
                                    <div class="scoreboard-score__divider">:</div>
                                    <div class="score__number-right">84</div>
                                </div>
                            </div>
                        </th>

                        <th class="table__cell table__cell-head">
                            <div class="team">
                                <div class="team__logo-wrapper logo-wrapper logo-wrapper--right">
                                    <img
                                        src="./../assets/team2-logo.png"
                                        alt="Банк Уралсиб"
                                        class="scoreboard__logo"
                                    >
                                </div>
                                <div class="table__team-name">Банк Уралсиб</div>
                            </div>
                        </th>
                    </tr>
                </thead>
                <TransitionGroup
                    tag="tbody"
                    name="list"
                    class="table__body"
                >
                    <tr
                        v-for="(item, index) in items"
                        :key="index"
                        class="table__row"
                    >
                        <td class="table__cell">
                            <div class="table__cell-content">
                                {{ item.col1 }}
                            </div>
                        </td>
                        <td class="table__cell">
                            <div class="table__cell-content table__cell-content-categories">
                                {{ item.col2 }}
                            </div>
                        </td>
                        <td class="table__cell">
                            <div class="table__cell-content">{{ item.col3 }}</div>
                        </td>
                    </tr>
                </TransitionGroup>
            </table>
        </div>

    </div>
</template>

<script setup>
import { ref, reactive, computed, onMounted, onUnmounted } from 'vue'

const teams = reactive({
    team1: { score: 0, showScore: false, showPhoto: false, showStats: false },
    team2: { score: 0, showScore: false, showPhoto: false, showStats: false },
})

const timeouts = {
    team1: { showScore: false, showPhoto: false, showStats: false },
    team2: { showScore: false, showPhoto: false, showStats: false },
};

const showMatchStatistics = ref(true);

const items = ref([
    { col1: "17/28 (61%)", col2: "2-х очковые", col3: "15/37 (41%)" },
    { col1: "11/39 (28%)", col2: "3-х очковые", col3: "15/35 (43%)" },
    { col1: "15/21 (71%)", col2: "Штрафные", col3: "10/14 (71%)" },
    { col1: "48", col2: "Подборы", col3: "36" },
    { col1: "13", col2: "Передачи", col3: "21" },
    { col1: "8", col2: "Перехваты", col3: "11" },
    { col1: "17", col2: "Потери", col3: "11" },
    { col1: "1", col2: "Блокшоты", col3: "1" }
])

const changeScore = (team, points) => {

    if (timeouts[team].showScore || timeouts[team].showPhoto || timeouts[team].showStats) {
        clearTimeout(timeouts[team].showScore);
        clearTimeout(timeouts[team].showPhoto);
        clearTimeout(timeouts[team].showStats);
        teams[team].showScore = false
        teams[team].showPhoto = false
        teams[team].showStats = false
    }

    teams[team].score = points;
    teams[team].showScore = true;

    timeouts[team].showScore = setTimeout(() => {
        teams[team].showScore = false
        teams[team].showStats = true
        timeouts[team].showPhoto = setTimeout(() => {
            teams[team].showPhoto = true
            timeouts[team].showStats = setTimeout(() => {
                teams[team].showPhoto = false
                teams[team].showStats = false
            }, 7000);
        }, 100);
    }, points * 1000);
}

</script>

<style scoped lang="scss">
/* Обнуление */
*,
::before,
::after {
    box-sizing: border-box;
}

input,
textarea,
select,
button {
    font: inherit;
}

:where(h1,
    h2,
    h3,
    h4,
    h5,
    h6):where([class]) {
    margin-block: 0;
}

/* Кнопки */

.right-team-buttons,
.left-team-buttons {
    position: absolute;
    top: 1vw;
    z-index: 200;

    display: flex;
    gap: .5vw;

    button {
        padding: 1vw 1.5vw;
        font-size: 1.3vw;
    }
}

.left-team-buttons {
    left: 1vw;
}

.right-team-buttons {
    right: 1vw;
}

.match-statistics-buttons {
    position: absolute;
    top: 6vw;
    z-index: 200;
    left: 1vw;
    font-size: 1.3vw;
}

/* Для анимации */

.scoreboard__logo-container {
    position: relative;
    width: 100%;
    height: 100%;
    overflow: hidden;
    transition: transform 1s ease-in-out;
}

.logo1--hidden {
    transform: translateX(-100%);
}

.logo2--hidden {
    transform: translateX(100%);
}

.scoreboard__score-text {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    background-color: var(--background-color);
    font-size: 3vw;
    font-weight: 600;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: opacity 1s ease-in-out;
    opacity: 0;
}

.scoreboard__score-text--left {
    color: var(--team-one-color);
}

.scoreboard__score-text--right {
    color: var(--team-two-color);
}

.score-text--shown {
    opacity: 1;
}

/* Transitions Slide */
.slide-fade-enter-active {
    transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
    transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
    transform: translateY(1vw);
    opacity: 0;
}

/* Transition Rotate */
.show-enter-active .scoreboard__content,
.show-leave-active .scoreboard__content {
    transition: transform 1.2s ease-in-out, opacity 1.8s ease-out;
}

/* Анимация табилицы в Match Statistics */
.list-enter-active,
.list-leave-active {
    transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: translateX(30px);
}

/* Основная табличка со счётом */
.scoreboard {
    --team-one-color: #FF6F06;
    --team-two-color: #0091FF;
    --inactive-color: #D9D9D9;
    --background-color: #fff;
    --text-color: #393939;

    position: relative;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;

    font-family: Helvetica;
    color: var(--text-color);

    /* временные свойства */
    background: transparent;

    font-size: 16px;
}


.scoreboard__main {
    position: absolute;
    z-index: 100;
    bottom: 2vw;
    width: calc(60vw);
    /* 65.7%; */
    height: 6%;
    /* 6%; */
    background: var(--background-color);
    color: var(--text-color);

    display: flex;
    align-items: center;
    justify-content: space-between;
    /* transform: translateY(100px); */
    /* transition: transform 0.5s ease-in-out; */

    -webkit-box-shadow: -3px 0px 23px -12px rgba(66, 68, 90, 1);
    -moz-box-shadow: -3px 0px 23px -12px rgba(66, 68, 90, 1);
    box-shadow: -3px 0px 23px -12px rgba(66, 68, 90, 1);
}

.scoreboard__team {
    flex: 1;
    display: flex;
    align-items: center;
    overflow: hidden;
    height: 100%;
    width: 30%;
}

.scoreboard__team--right {
    justify-content: end;
}

.scoreboard__team-name-wrapper {
    width: 90%;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
}

.scoreboard__team-name {
    width: 100%;
    padding: .6vw .1vw;
    border-radius: 45px;

    text-align: center;
    font-family: Helvetica;
    font-size: calc(1.8vw / (16 / 9));
    font-style: normal;
    font-weight: 600;
    line-height: normal;

    display: flex;
    align-items: center;
    justify-content: center;
}

.scoreboard__team--right .scoreboard__team-name {
    border: 1.2vw solid var(--team-two-color);
}

.scoreboard__team--left .scoreboard__team-name {
    border: 1.2vw solid var(--team-one-color);
}

.logo-wrapper {
    padding: 6%;
    background-color: var(--background-color);
    border-radius: 50%;
    overflow: hidden;

    display: flex;
    align-items: center;
    justify-content: center;
}

.scoreboard__logo-wrapper {
    width: 9%;
    aspect-ratio: 1 / 1;
    padding: 1%;
}

.scoreboard__logo-wrapper,
.team__logo-wrapper {
    position: absolute;
}

.scoreboard__team--left .scoreboard__logo-wrapper {
    right: 95%;
}

.scoreboard__team--right .scoreboard__logo-wrapper {
    left: 95%;
}

.logo-wrapper--left {
    border: .4vw solid var(--team-one-color);
}

.logo-wrapper--right {
    border: .4vw solid var(--team-two-color);
}

.scoreboard__logo {
    width: 100%;
}

.score {
    position: relative;
}

.score::after {
    content: '';
    position: absolute;
    z-index: 5;
    bottom: 50%;
    left: 50%;
    transform: translateX(-50%);
    background: var(--team-two-color);
    height: .1vw;
    width: 24.5vw;
}

.score-inner {
    text-align: center;
    font-family: Helvetica;
    font-size: 1.3vw;
    font-style: normal;
    font-weight: 600;
    line-height: normal;

    background: var(--background-color);
    border: 1px solid var(--team-two-color);
    border-radius: 135.242px;

    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    z-index: 10;
}

.scoreboard-score-inner {
    margin: 0 .4vw;
    padding: .3vw .1vw;
    width: 8vw;

}

.scoreboard-score__divider {
    margin: 0 5px;
    flex: 0
}

.score__number-left,
.score__number-right {
    flex: 1;
}

.score__number-right {
    text-align-last: left;
}

.score__number-left {
    text-align-last: right;
}

.scoreboard__indicators {
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 14%;
    height: 100%;

    align-items: flex-end;
}

.scoreboard__indicators-right {
    margin-left: 1vw;
}

.scoreboard__indicators-left {
    margin-right: 1vw;
}

.scoreboard__line {
    display: flex;
    gap: 2px;
}

.scoreboard__dash {
    display: inline-block;
    width: calc(2.25vw / (16 / 9));
    height: .2vw;
    flex-shrink: 0;
    border-radius: 88.567px;
    background: var(--inactive-color);
}

.scoreboard__indicators-left .scoreboard__dash--active {
    background: var(--team-one-color);
}

.scoreboard__indicators-right .scoreboard__dash--active {
    background: var(--team-two-color);
}

.scoreboard__bottom-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
}

.scoreboard-scores {
    display: flex;
    align-items: center;
    gap: .2vw;
}

.scoreboard__number {
    text-align: center;
    font-size: .6vw;
    font-style: normal;
    font-weight: 600;
    line-height: normal;
    position: relative;
    display: flex;
    align-items: center;
    color: var(--inactive-color);
}

.scoreboard__indicators-left .scoreboard__number--active {
    color: var(--team-one-color);
}

.scoreboard__indicators-right .scoreboard__number--active {
    color: var(--team-two-color);
}

.scoreboard__number:not(:last-child)::after {
    content: '-';
    position: absolute;
    left: 107%;
    top: -1px;
}

.scoreboard__circles {
    display: flex;
    align-items: center;
    gap: 2px;
}

.scoreboard__circle {
    display: inline-block;
    border-radius: 50%;
    width: .4vw;
    aspect-ratio: 1;
    background: var(--inactive-color);
}

.scoreboard__indicators-left .scoreboard__circle--active {
    background: var(--team-one-color);
}

.scoreboard__indicators-right .scoreboard__circle--active {
    background: var(--team-two-color);
}


.scoreboard__overlay {
    position: absolute;
    z-index: 20;
    bottom: 5vw;

    display: flex;
    align-items: center;
    justify-content: center;

    width: 8vw;
    background: var(--background-color);
    padding-top: calc(.9vw / (16 / 9));
    padding-bottom: calc(.9vw / (16 / 9));
    border-radius: 1.5vw 1.5vw 0 0;

    color: var(--team-two-color);
    font-size: 1.2vw;

    /* transform: rotateX(90deg); */
    transform-origin: bottom;
    transition: transform 0.5s ease-in-out;
}

.scoreboard__quarter {
    background-color: var(--team-two-color);
    color: var(--background-color);
    width: 1.7vw;
    aspect-ratio: 1 / 1;
    border-radius: 50%;

    display: flex;
    align-items: center;
    justify-content: center;

    font-size: 1vw;
    font-weight: 600;
}

.scoreboard__divider {
    height: 1.3vw;
    width: .05vw;
    background-color: var(--team-two-color);
    margin: 0 .5vw;
}

.scoreboard__player-info {
    position: absolute;
    bottom: 5vw;
    width: 20.5vw;
    aspect-ratio: 22/1;
    font-size: .7vw;
    font-weight: 600;

}

.scoreboard__player-info-inner {
    background-color: var(--background-color);
    padding: calc(0.6vw / (16 / 9)) calc(2vw / (16 / 9));
    border-radius: 1.5vw 1.5vw 0 0;

    display: flex;
    align-items: start;
    gap: .2vw;
}

.scoreboard__player-info-inner-left {
    justify-content: end;
}

.scoreboard__player-info--right {
    transform: translateX(78%);
}

.scoreboard__player-info--right .scoreboard__player-name {
    text-align: right;
}

.scoreboard__player-name {
    width: 7vw;
    aspect-ratio: 4 / 1;
    text-align: left;
}

.scoreboard__player-photo-wrapper {
    width: 4vw;
    aspect-ratio: 1 / 1;
    border-radius: 50px;

    display: flex;
    align-items: center;
    justify-content: center;

    overflow: hidden;
}

.scoreboard__player-photo {
    height: 100%;
}

.scoreboard__player-info--right .scoreboard__player-photo-wrapper {
    left: 90%;
    bottom: 20%;
}

.scoreboard__player-info--left {
    transform: translateX(-78%);
}

.scoreboard__player-info--left .scoreboard__player-photo-wrapper {
    right: 90%;
    bottom: 20%;
}


.scoreboard__player-stats {
    display: flex;
    gap: calc(.7vw /(16 / 9));
}

.scoreboard__stat {
    display: flex;
    flex-direction: column;
    align-items: start;
}

.scoreboard__player-photo-wrapper {
    position: absolute;
}

/* Общая статистика */
.scoreboard__content {
    position: absolute;
    top: calc(50% - 4vw);
    left: 50%;
    width: 58%;
    height: 70%;

    display: flex;
    justify-content: center;

    background-color: var(--background-color);
    padding: 1.5%;
    border-radius: 12px;

    font-weight: 600;

    background-image: url('./../assets/table-image.png');
    background-size: 75%;
    background-position: 125% 70%;
    background-repeat: no-repeat;

    transition: transform 1.2s ease-in-out, opacity 0.8s ease-out;
    transform: translate(-50%, -50%);
}

.scoreboard__content--hidden {
    transform: translate(-50%, 100%);
    opacity: 0;
}

.table {
    border-spacing: calc(1vw / (16 / 9));
    width: 98%;
}

.table__caption {
    width: 46%;
    aspect-ratio: 6 / 1;
    padding: .1em;
    margin-bottom: 2%;
    display: flex;
    align-items: center;
    justify-content: center;

    text-align: center;
    color: var(--text-color);
    font-style: normal;
    font-size: 2.3vw;
    font-weight: 600;
    line-height: normal;

    border-radius: 105.799px;
    background: var(--background-color);
    box-shadow: 0px 7.053px 17.633px 0px rgba(0, 0, 0, 0.10);

}

.table__row {
    display: flex;
    justify-content: space-between;
    margin-bottom: calc(.9vw / (16 / 9));
}

.table__row-head {
    margin-bottom: calc(1.8vw / (16 / 9));
}

.table__cell-content {
    display: flex;
    align-items: center;
    justify-content: center;
}

.table__row td:nth-child(2),
.table__row-head th:nth-child(2) {
    font-weight: bold;
    width: 50%;

    display: flex;
    justify-content: center;
}

.team {
    position: relative;
    width: 12vw;
    aspect-ratio: 6 / 1;
}

.table__cell-content:nth-child(1),
.table__cell-content:nth-child(3) {
    color: var(--background-color);
    border-radius: 1vw;
    width: 11vw;
    aspect-ratio: 5 / 1;
}

.table__cell:nth-child(1) .table__cell-content {
    background: var(--team-one-color);
}

.table__cell:nth-child(3) .table__cell-content {
    background: var(--team-two-color);
}

.table__cell-content.table__cell-content-categories {
    border: .05vw solid var(--text-color);
    border-radius: 30px;
    background-color: var(--background-color);
    color: var(--text-color);
    padding: calc(0.01vw / (16 / 9)) 0;
    width: 50%;

    font-size: calc(2.4vw / (16 / 9));
    aspect-ratio: 7 / 1;
    position: relative;
}

.table__cell-content-categories::before,
.table__cell-content-categories::after {
    content: '';
    position: absolute;
    top: 50%;
    height: .1vw;
    width: 50%;
}

.table__cell-content-categories::before {
    background-color: var(--team-one-color);
    right: 100%;
}

.table__cell-content-categories::after {
    background-color: var(--team-two-color);
    left: 100%;
}

.table__cell-head {
    width: 11vw;
    background-color: transparent;
    display: flex;
    align-items: center;
}

.table__team-name {
    position: absolute;
    z-index: 10;
    width: 100%;
    aspect-ratio: 12 / 2;
    background: var(--background-color);
    border-radius: 1vw;
    box-shadow: 0px 7.053px 17.633px 0px rgba(0, 0, 0, 0.10);

    display: flex;
    align-items: center;
    justify-content: center;

    font-size: 1vw;
    font-weight: 600;
    color: var(--text-color);
}

.table__cell-content {
    font-size: 1.1vw;
}

.table__cell-head:nth-child(1) .table__team-name {
    transform: translateX(15%);
}

.table__cell-head:nth-child(3) .table__team-name {
    transform: translateX(-15%);
}

.table__cell-content:nth-child(2) {
    margin: 0 auto;
}

.team__logo-wrapper {
    z-index: 15;
    width: 45%;
    height: unset;
    aspect-ratio: 1 / 1;
}

.team__logo-wrapper.logo-wrapper--left {
    bottom: -50%;
    left: -17%;
}

.team__logo-wrapper.logo-wrapper--right {
    bottom: -50%;
    right: -17%;
}

.table-score {
    width: 50%;
}

.table-score::after {
    width: 200%;
}

.table-score-inner {
    padding: 3%;
    font-size: calc(3.5vw / (16 / 9));
}
</style>