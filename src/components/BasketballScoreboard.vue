<template>

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

    <div class="scoreboard">

        <!-- Основная табличка со счетом -->
        <div class="scoreboard__main">
            <div class="scoreboard__team scoreboard__team--left">
                <div class="scoreboard__logo-wrapper logo-wrapper logo-wrapper--left">
                    <div
                        class="scoreboard__logo-container"
                        :class="{ 'logo1--hidden': teams.team1.showText }"
                    >
                        <img
                            src="./../assets/team1-logo.png"
                            alt="BIP Lions"
                            class="scoreboard__logo"
                        />
                    </div>
                    <div
                        class="scoreboard__score-text"
                        :class="{ 'score-text--shown': teams.team1.showText }"
                    >
                        +{{ teams.team1.score }}
                    </div>
                </div>
                <div class="scoreboard__team-name-wrapper">
                    <div class="scoreboard__team-name">BIP Lions</div>
                </div>
            </div>
            <div class="scoreboard__indicators scoreboard__indicators--left">
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
                    <div class="scoreboard-score__left-number">186</div>
                    <div class="scoreboard-score__divider">:</div>
                    <div class="scoreboard-score__right-number">184</div>
                </div>
            </div>
            <div class="scoreboard__indicators scoreboard__indicators--right">
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
                        :class="{ 'logo2--hidden': teams.team2.showText }"
                    >
                        <img
                            src="./../assets/team2-logo.png"
                            alt="BIP Lions"
                            class="scoreboard__logo"
                        />
                    </div>
                    <div
                        class="scoreboard__score-text scoreboard__score-text--right"
                        :class="{ 'score-text--shown': teams.team2.showText }"
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
                    class="scoreboard__player-info-inner"
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
                    <tr class="table__row table__row--head">

                        <th class="table__cell table__cell--head">

                            <div class="scoreboard__team--left">
                                <div class="table__logo-wrapper logo-wrapper logo-wrapper--left">
                                    <img
                                        src="./../assets/team1-logo.png"
                                        alt="BIP Lions"
                                        class="scoreboard__logo"
                                    >
                                </div>
                                <div class="table__team-name">BIP Lions</div>
                            </div>

                        </th>

                        <th class="table__cell table__cell--head">
                            <div class="score table-score">
                                <div class="score-inner table-score-inner">
                                    <div class="scoreboard-score__left-number">186</div>
                                    <div class="scoreboard-score__divider">:</div>
                                    <div class="scoreboard-score__right-number">184</div>
                                </div>
                            </div>
                        </th>

                        <th class="table__cell table__cell--head">
                            <div class="scoreboard__team--right">
                                <div class="table__logo-wrapper logo-wrapper logo-wrapper--right">
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
                        <td class="table__cell">{{ item.col1 }}</td>
                        <td class="table__cell">
                            <div class="table__cell-categories">
                                {{ item.col2 }}
                            </div>
                        </td>
                        <td class="table__cell">{{ item.col3 }}</td>
                    </tr>
                </TransitionGroup>
            </table>
        </div>

    </div>
</template>

<script setup>
import { ref, reactive } from 'vue'

const teams = reactive({
    team1: { showText: false, score: 0, showPhoto: false, showStats: false },
    team2: { showText: false, score: 0, showPhoto: false, showStats: false },
})

const showMatchStatistics = ref(true);

const changeScore = (team, points) => {
    console.log('changeScore', team);

    teams[team].score = points;
    teams[team].showText = true;

    setTimeout(() => {
        teams[team].showText = false
        teams[team].showStats = true
        setTimeout(() => {
            setTimeout(() => {
                teams[team].showPhoto = true
                setTimeout(() => {
                    teams[team].showPhoto = false
                    teams[team].showStats = false
                }, 7000);
            }, 100);
        }, 100);
    }, points * 1000);
}

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
</script>

<style scoped>
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
    top: 20px;
    z-index: 200;

    display: flex;
    gap: 5px;
}

.left-team-buttons {
    left: 20px;
}

.right-team-buttons {
    right: 20px;
}

.match-statistics-buttons {
    position: absolute;
    top: 100px;
    z-index: 200;
    left: 20px;
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
    font-size: 2rem;
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
    transform: translateY(20px);
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

    position: fixed;
    bottom: 0;
    right: 0;
    left: 0;
    top: 0;
    display: flex;
    flex-direction: column;
    align-items: center;

    perspective: 10000px;
    /* Добавляет глубину 3D */

    font-family: Helvetica;
    color: var(--text-color);

    /* временные свойства */
    background: rgb(0, 120, 0);
}

.scoreboard__main {
    position: absolute;
    z-index: 100;
    bottom: 33px;
    width: calc(900px - 2 * 25px);
    /* 65.7%; */
    height: 45px;
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
}

.scoreboard__team--right {
    justify-content: end;
}

.scoreboard__team-name-wrapper {
    overflow: hidden;
    height: 45px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.scoreboard__team-name {
    width: 215px;
    padding: 8px 20px;
    border-radius: 45px;

    text-align: center;
    font-family: Helvetica;
    font-size: 18.06px;
    font-style: normal;
    font-weight: 600;
    line-height: normal;

    display: flex;
    align-items: center;
    justify-content: center;
}

.scoreboard__team--right .scoreboard__team-name {
    border: 20px solid var(--team-two-color);
    margin-right: 25px;
}

.scoreboard__team--left .scoreboard__team-name {
    border: 20px solid var(--team-one-color);
    margin-left: 25px;
}

.logo-wrapper {
    width: 70px;
    height: 70px;
    padding: 10px;
    background-color: var(--background-color);
    border-radius: 50%;
    overflow: hidden;

    display: flex;
    align-items: center;
    justify-content: center;
}

.scoreboard__logo-wrapper,
.table__logo-wrapper {
    position: absolute;
}

.scoreboard__team--left .scoreboard__logo-wrapper {
    left: -12px;
}

.scoreboard__team--right .scoreboard__logo-wrapper {
    right: -12px;
}

.logo-wrapper--left {
    border: 6px solid var(--team-one-color);
}

.logo-wrapper--right {
    border: 6px solid var(--team-two-color);
}

.scoreboard__logo {
    width: 40px;
    height: 40px;
}

.score {
    position: relative;
}

.score::after {
    content: '';
    position: absolute;
    z-index: 5;
    bottom: 16px;
    left: 50%;
    transform: translateX(-50%);
    background: var(--team-two-color);
    height: 1px;
    width: 351px;
}

.score-inner {
    text-align: center;
    font-family: Helvetica;
    font-size: 18.06px;
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
    margin: 0 7px;
    height: 33px;
    width: 120px;
}

.scoreboard-score__divider {
    margin: 0 5px;
    flex: 0
}

.scoreboard-score__left-number,
.scoreboard-score__right-number {
    flex: 1;
}

.scoreboard-score__right-number {
    text-align-last: left;
}

.scoreboard-score__left-number {
    text-align-last: right;
}

.scoreboard__indicators {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 25px;

    transform: translateY(3px);
}

.scoreboard__line {
    display: flex;
    gap: 2px;
}

.scoreboard__dash {
    display: inline-block;
    width: 20px;
    height: 4px;
    flex-shrink: 0;
    border-radius: 88.567px;
    background: var(--inactive-color);
}

.scoreboard__indicators--left .scoreboard__dash--active {
    background: var(--team-one-color);
}

.scoreboard__indicators--right .scoreboard__dash--active {
    background: var(--team-two-color);
}

.scoreboard__bottom-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.scoreboard-scores {
    display: flex;
    align-items: center;
    gap: 5px;
}

.scoreboard__number {
    text-align: center;
    font-size: 12px;
    font-style: normal;
    font-weight: 600;
    line-height: normal;
    position: relative;
    display: flex;
    align-items: center;
    color: var(--inactive-color);
}

.scoreboard__indicators--left .scoreboard__number--active {
    color: var(--team-one-color);
}

.scoreboard__indicators--right .scoreboard__number--active {
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
    width: 6px;
    height: 6px;
    background: var(--inactive-color);
}

.scoreboard__indicators--left .scoreboard__circle--active {
    background: var(--team-one-color);
}

.scoreboard__indicators--right .scoreboard__circle--active {
    background: var(--team-two-color);
}


.scoreboard__overlay {
    position: absolute;
    bottom: 73px;

    display: flex;
    align-items: center;
    justify-content: center;

    width: 120px;
    background: var(--background-color);
    padding-top: 6px;
    padding-bottom: 5px;
    border-radius: 25px 25px 0px 0px;

    color: var(--team-two-color);
    font-size: 18px;

    /* transform: rotateX(90deg); */
    transform-origin: bottom;
    transition: transform 0.5s ease-in-out;
}

.scoreboard__quarter {
    background-color: var(--team-two-color);
    color: var(--background-color);
    width: 24px;
    height: 24px;
    padding: 5px;
    border-radius: 50px;

    display: flex;
    align-items: center;
    justify-content: center;

    font-size: 20px;
    font-weight: 600;
}

.scoreboard__divider {
    height: 24px;
    width: 1px;
    background-color: var(--team-two-color);
    margin: 0 5px;
}

.scoreboard__player-info {
    position: absolute;
    bottom: 73px;
    width: 310px;
    height: 40px;

    font-size: 10px;
    font-weight: 600;

}

.scoreboard__player-info-inner {
    background-color: var(--background-color);
    padding: 5px 25px;
    border-radius: 25px 25px 0 0;

    display: flex;
    align-items: start;
    gap: 8px;
}

.scoreboard__player-info--right {
    transform: translateX(78%);
    padding-right: 30px;
}

.scoreboard__player-info--right .scoreboard__player-name {
    text-align: right;
}

.scoreboard__player-name {
    width: 82px;
    height: 30px;
    text-align: left;
}

.scoreboard__player-photo-wrapper {
    width: 51px;
    height: 51px;
    border-radius: 50px;

    display: flex;
    align-items: center;
    justify-content: center;

    overflow: hidden;
}

.scoreboard__player-photo {
    height: 51px;
}

.scoreboard__player-info--right .scoreboard__player-photo-wrapper {
    left: 83%;
    bottom: 20%;
}

.scoreboard__player-info--left {
    transform: translateX(-78%);
    padding-left: 30px;
}

.scoreboard__player-info--left .scoreboard__player-photo-wrapper {
    right: 83%;
    bottom: 20%;
}


.scoreboard__player-stats {
    display: flex;
    gap: 8px;
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
    top: calc(50% - (40px + 45px + 33px) / 2);
    /* top: 50%; */
    left: 50%;
    width: 800px;
    height: 600px;

    background-color: var(--background-color);
    padding: 35px 30px 10px;
    border-radius: 12px;

    font-weight: 600;

    background-image: url('./../assets/table-image.png');
    background-size: 620px;
    background-position: 125% 70%;
    background-repeat: no-repeat;

    transition: transform 1.2s ease-in-out, opacity 0.8s ease-out;
    /* transform:  */

    transform-style: preserve-3d;
    transform: translate(-50%, -50%) perspective(900px);
}

.scoreboard__content--hidden {
    transform: rotate3d(1, 0, 0, 90deg) translate3D(-50%, 0px, -110px);
    opacity: 0;
}

.table {
    border-spacing: 15px;
}

.table__caption {
    height: 70px;
    width: 500px;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    justify-content: center;

    text-align: center;
    color: var(--text-color);
    font-size: 40px;
    font-style: normal;
    font-weight: 600;
    line-height: normal;

    border-radius: 105.799px;
    background: #FFF;
    box-shadow: 0px 7.053px 17.633px 0px rgba(0, 0, 0, 0.10);
}

.table__row td:nth-child(2),
.table__row--head th:nth-child(2) {
    font-weight: bold;
    width: 360px;

    display: flex;
    justify-content: center;
}

.table__cell:nth-child(1),
.table__cell:nth-child(3) {
    color: var(--background-color);
    border-radius: 20px;
    width: 250px;
}

.table__cell:nth-child(1) {
    background: var(--team-one-color);
}

.table__cell:nth-child(3) {
    background: var(--team-two-color);
}

.table__cell-categories {
    border: 1px solid var(--text-color);
    border-radius: 30px;
    background-color: var(--background-color);
    padding: 1px 0;
    width: 180px;

    font-size: 19px;
    position: relative;
}

.table__cell-categories::before,
.table__cell-categories::after {
    content: '';
    position: absolute;
    top: 50%;
    height: 1px;
    width: 85px;
}

.table__cell-categories::before {
    background-color: var(--team-one-color);
    right: 100%;
}

.table__cell-categories::after {
    background-color: var(--team-two-color);
    left: 100%;
}

.table__cell.table__cell--head {
    background-color: transparent;
}

.table__team-name {
    position: absolute;
    top: 12px;
    z-index: 10;
    width: 160px;
    height: 30px;
    background: var(--background-color);
    border-radius: 20px;
    box-shadow: 0px 7.053px 17.633px 0px rgba(0, 0, 0, 0.10);

    display: flex;
    align-items: center;
    justify-content: center;

    font-size: 13px;
    font-weight: 600;
    color: var(--text-color);
}

.table__cell.table__cell--head:nth-child(1) {
    transform: translateX(17px);
}

.table__cell.table__cell--head:nth-child(3) {
    transform: translateX(-17px);
}

.table__logo-wrapper {
    z-index: 15;
}

.table__logo-wrapper.logo-wrapper--left {
    top: -20%;
    left: -32%;
}

.table__logo-wrapper.logo-wrapper--right {
    top: -20%;
    right: -32%;
}

.table-score-inner {
    font-size: 28px;
    width: 180px;
    height: 50px;
}

.table-score::after {
    bottom: 22px;
}
</style>