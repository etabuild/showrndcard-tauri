<template>
    <div id="header">
        <p>ランダムなカードを表示</p>
    </div>
    <div id="content">

        <div id="view_container">
            <div id="item_history">
                <p v-if="isempty" id="label_history">履歴なし</p>
                <p v-if="isempty==false" id="label_history">履歴</p>
                <div id="showedList">


                    <div v-for="id in imghistory" @click="historyClick(id)" class="historyblock">
                        <p class="historylabel" v-html="'imgid: '+id"></p>
                        <img class="historyimg"
                             v-bind:src="'https://dm.takaratomy.co.jp/wp-content/card/cardthumb/'+list[id]">
                    </div>
                </div>
            </div>
            <div id="item_button">
                <button id="b_generate" @click="gen">ここを押そうね☆</button>
                <p v-html="'imgid: '+imgnum" id="imgid"></p>

            </div>
            <div id="item_viewer">
                <div id="img_wrapper">
                    <img id="card" :src="imgsrc">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            list: null,
            imgnum: 0,
            imgsrc: "https://dm.takaratomy.co.jp/wp-content/card/cardthumb/dm22sp2-004.jpg",
            imghistory: [],
            isempty: true

        }
    },
    name: "Main.vue",
    created() {
        this.imgel = document.getElementById("card")
        axios.get('https://cardpickrandom.008900011055q3f.repl.co/data/list.json')
            .then(function (response) {
                //デバッグ用にconsoleに出力
                console.log(response.data.imgpath[0])
                this.list = response.data.imgpath
            }.bind(this))
            .catch(function (error) {
                alert('jsonの読み込みに失敗しました。再読み込みしてそれでも無理だったら明日試そうね☆')
                console.log(error)
            })
    },
    methods: {
        historyClick: function (id) {
            this.genbyid(id)
        },
        gen: function () {
            var random = Math.floor(Math.random() * 15760);
            this.imgnum = random
            this.imghistory.push(random)
            this.isempty = false
            this.imgsrc = 'https://dm.takaratomy.co.jp/wp-content/card/cardthumb/' + this.list[random]
            var box = document.getElementById('showedList')
            box.scrollTo(0, box.scrollHeight);
        },
        genbyid: function (id) {
            this.isempty = false
            this.imgnum = id
            this.imgsrc = 'https://dm.takaratomy.co.jp/wp-content/card/cardthumb/' + this.list[id]

        }
    }
}


</script>

<style scoped>

#label_history {
    color: #fff;
    position: absolute;
    top: 0;
    left: 30%;
    right: 30%;
    height: 28px;
    border-radius: 13px;
    /*
    border: solid 1px #000;
    */
    margin-top: 12px;
    /*
    width: 60px;
    */
    z-index: 19;
    background: rgba(87, 63, 236, 1)


}

#item_history {
    position: absolute;
    grid-row: 2/3;
    grid-column: 1/2;
    left: 0;
    top: 0;
    bottom: 0;
    width: 100%;
}

#item_viewer {
    grid-row: 2/3;
    grid-column: 2/3;
    /*
    height: 100%
    */
}

#item_button {
    grid-row: 1/2;
    grid-column: 1/3;
}

#img_wrapper{
    width: 100%;
    text-align: left;
    margin-left: 5%;
}
body {
    margin: 0;
    padding: 0;
    font-weight: normal;
    font-family: Line_Seed_JP;

}

body.no_scroll {
    overflow: hidden;
}

.historyimg {
    height: 140px;
    padding: 8px;
}

.historylabel {
    position: absolute;
    top: 10px;
    left: 10px;
    background-color: rgba(232, 232, 232, 0.71);
    font-size: 0.8em;
}

.historyblock {
    min-height: 20px;
    background-color: #e8e8e8;
    margin: 7px;
    border-radius: 8px;
    font-family: Line_Seed_JP;
    font-weight: normal;
    border: solid 2px #fff;
    position: relative;
    transition: .1s;
}

.historyblock:hover {
    border: solid 2px #000000;
    transition: .5s;
}


#showedList {
    padding-top: 40px;
    width: 100%;
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    background-color: rgba(255, 255, 255, 0.47);
    border: solid 2px #573fec;
    border-radius: 10px;
    overflow-y: scroll;
    overflow-x: hidden;

}

#card {
    margin: 0 auto;
    text-align: left;
    /*width: 90%;
    max-width: 30vw;
    min-width: 300px;*/
    /*
    height: 65vh;
    */
    width: 70%;

}

#header {
    color: #573fec;
    z-index: 20;
    text-align: center;
    /*
    border-bottom: solid #000 1px;
    */
    font-family: Line_Seed_JP;
    font-weight: 900;
    font-size: 2em;
    width: 100vw;
    /*    position: fixed;
        top: 0;
        left: 0;
        right: 0;*/
    height: 12vh;
    line-height: 12vh;
    /*
    background: rgba(255, 255, 255, 0.47)
    */
    background: #e0dcfd;

}


#content {
    /*
    padding: 0 18vw 0 18vw;
    */
    text-align: center;
    max-height: 100vh;
    font-family: Line_Seed_JP;
    /*
    display: flex;
    */
}

#b_generate {
    display: block;
    font-family: Line_Seed_JP;

    margin: 10px auto 0px auto;

    padding: 5px;
    width: 200px;
    font-size: 1.4em;
    background: none;
    border-radius: 10px;
    border: none;
    transition: .2s
}

#b_generate:hover {
    /*background: #6737FFFF;*/
    border: solid 0px;
    text-shadow: #6737FFFF 0px 0 10px;
    transition: .1s;
}

#view_container {
    padding: 20px;
    position: relative;
    display: grid;
    grid-template-rows: 1fr 4.5fr;
    grid-template-columns: 1fr 2fr;
    height: 70vh;
    width: 55%;
    margin: 0 auto;
}


.historyblock p {
    margin: 0;
}

#imgid {
    margin: 0;
}



@media screen and (max-width: 860px) {
    #view_container{
        width: 90%;

    }
}

@media screen and (max-width: 480px) {
    #view_container {
        display: block;


    }

    #header{
        font-size: 1.3em;
    }
    #card {
        width: 90%;
        height: auto;
    }

    #item_history{
        display: none;
    }


}



</style>