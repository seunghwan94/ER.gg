<template>
    <div class="main-search-recode" :style="{ backgroundImage: 'url(' + openimg() + ')' }">
        <div style="font-size: 14px;">
            <span style="font-weight: bold;" v-bind:style="{color: 
            datalist.gameRank === 1 ? 'red' :
            datalist.gameRank === 2 || datalist.gameRank === 3 ? 'blue' : 'gray'
            }">{{datalist.gameRank}}위</span>&nbsp;
            {{ datalist.matchingMode === 2 ? '일반' : '랭크' }} {{ formatTime(datalist.playTime) }}
        </div>
        <hr/>
        <div style="display:flex;width:100%;justify-content: space-between;align-items: center;">
            <div style="display: flex;align-items: center;">
                <div>
                    <img class="tier-img" :src="`${datalist.skinUrl}`" style="padding-bottom: 0px;"/> <br/>{{ datalist.characterName }}
                </div>
                <div style="margin: 0 15px;">
                    <div style="font-size: 14px;font-weight: bold;margin-bottom: 5px;">{{ datalist.teamKill }} / {{ datalist.playerKill }} / {{ datalist.playerAssistant }}</div>
                    <div style="font-size: 12px;color: gray;margin-bottom: 5px;"> TK / K / A</div>
                    <div>
                        <div style="font-size: 12px;color: gray;">평점(KDA) <span style="font-weight: bold;color: black;">{{ datalist.kda }}</span></div>
                    </div>
                </div>
            </div>
            <div>
            </div>
            <div style="margin: 0 15px;display: flex;flex-direction: column;width: 20%;font-size: 14px;">
                <div style="display: flex;justify-content: flex-end;align-items: center;">
                     <div style="display: flex;font-weight: bold;margin-bottom: 10px;">Lv {{ datalist.characterLevel }}</div>
                </div>
                <div style="display: flex;justify-content: space-between;;align-items: center;">
                    <div style="font-size: 12px;color: gray;">딜량</div>
                    <div style="font-weight: bold">{{ datalist.damageToPlayer }}</div>
                </div>
                <div style="display: flex;justify-content: space-between;;align-items: center;">
                    
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import { Character } from '../../config.json'

export default {
    data() {
        return {
            Character:Character,
        };
    },
    props:{
        datalist:Object
    },
    methods: {
        formatTime(time) {
        const hours = Math.floor(time / 100); // 시간
        const minutes = time % 100; // 분
        return `${hours} : ${minutes < 10 ? '0' + minutes : minutes}`;
        },
        openimg(){
            const characterName = this.datalist.characterName;
            const keys = Object.keys(Character);
            const index = keys.indexOf(characterName) + 1;
            const paddedIndex = index.toString().padStart(3, '0');

            return 'https://cdn.dak.gg/er/images/character/background/bg_char' + paddedIndex + '.jpg';
        },
    }
}
</script>
<style>
.main-search-recode {
    border: 2px solid gray;
    width: 94%;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 10px;
    margin: 10px 0;
    /* background: url('https://cdn.dak.gg/er/images/character/background/bg_char047.jpg'); */
}
</style>