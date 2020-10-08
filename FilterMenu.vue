<template>
    <div >
        <div class="background"></div>
        <div class="white-bg1">
            <div class="kind-dish">
                <div 
                :class="{active: dishKind == 'drinks'}" 
                data-circle="drinks" class="drink circle"
                @click="dishKind = 'drinks'">
                    <img src="../assets/filter/drinks.svg" alt="">
                </div>
                <div :class="{active: dishKind == 'main'}" 
                data-circle="main dish" class="main circle"
                @click="dishKind = 'main'">
                    <img class="main-img" src="../assets/filter/main.svg" alt="">
                </div>
                <div :class="{active: dishKind == 'desserts'}" 
                data-circle="desserts" class="dessert circle"
                @click="dishKind = 'desserts'">
                    <img src="../assets/filter/desserts.svg" alt="">
                </div>
            </div>
           <h1>filter</h1>
        </div>

        <section id="prods"  
        ref="prods"  
        class="white-bg2">
            <div id="mydivheader" class="container">
        
                <div  class="block " >
                    <div @click="promo = !promo" id="prodspromo" class="square">
                        <img  :src="require(`../assets/filter/promo${promo?'Red':''}.svg`)" alt="">
                        <p :class="{active: promo}">promo</p>
                    </div>
                </div>
                <div  class="block ">
                    <div @click="vegan = !vegan" id="prodsvegan" class="square">
                        <img :src="require(`../assets/filter/vegan${vegan?'Red':''}.svg`)" alt="">
                        <p :class="{active: vegan}">vegan</p>
                    </div>
                </div>

                <div class="block " >
                    <div @click="dairyFree = !dairyFree" id="prodsdairy-free" class="square">
                        <img :src="require(`../assets/filter/dairy-free${dairyFree?'Red':''}.svg`)" alt="">
                        <p :class="{active: dairyFree}">dairy-free</p>
                    </div>
                </div>
                <div class="block " >
                    <div @click="vegetarian = !vegetarian" id="prodsvegetarian" class="square">
                        <img class="milk" :src="require(`../assets/filter/vegetarian${vegetarian?'Red':''}.svg`)" alt="">
                        <p :class="{active: vegetarian}">vegetarian</p>
                    </div>
                </div>
                <div class="block " >
                    <div @click="halal = !halal" id="prodshalal" class="square">
                        <img :src="require(`../assets/filter/halal${halal?'Red':''}.svg`)" alt="">
                        <p :class="{active: halal}">halal</p>
                    </div>
                </div>
                <div class="block " >
                    <div @click="kosher = !kosher" id="prodskosher" class="square">
                        <img :src="require(`../assets/filter/kosher${kosher?'Red':''}.svg`)" alt="">
                        <p :class="{active: kosher}">kosher</p>
                    </div>
                </div>
                <div class="block ">
                    <div @click="glutenFree = !glutenFree" id="prodsgluten-free" class="square">
                        <img :src="require(`../assets/filter/gluten-free${glutenFree?'Red':''}.svg`)" alt=""> 
                        <p :class="{active: glutenFree}">gluten-free</p>             
                    </div>
                </div>
                <div  class="block " >
                    <div @click="nutFree = !nutFree"  id="prodsnut-free" class="square">
                        <img :src="require(`../assets/filter/nut-free${nutFree?'Red':''}.svg`)" alt="">
                        <p :class="{active: nutFree}">nut-free</p>
                    </div>
                </div>
                
            </div>
        </section>

        <div id="calor" class="white-bg3">
            <div class="container">
        
                <div @click="currentCalories = 150"  class="block">
                    <div id="calor150" class="calories">
                        <p>150</p>
                    </div>
                </div>
                <div @click="currentCalories = 300" class="block">
                    <div id="calor300" class="calories">
                        <p>300</p>
                    </div>
                </div>

                <div @click="currentCalories = 500" class="block">
                    <div id="calor500" class="calories">
                        <p>500</p>
                    </div>
                </div>
                <div class="block">
                     <div class="calories active">
                        <transition name="fadeIn">
                            <p v-if="currentCalories">{{currentCalories}}</p>
                        </transition>
                        
                    </div>
                </div>
                <div @click="currentCalories = 800" class="block">
                    <div id="calor800" class="calories">
                        <p>800</p>
                    </div>
                </div>
                <div @click="currentCalories = 1000" class="block">
                     <div id="calor1000" class="calories">
                        <p>1000</p>
                    </div>
                </div>
                <div @tclick="currentCalories = 1500" class="block">
                     <div id="calor1500" class="calories">
                        <p>1500</p>
                    </div>
                </div>
                
            </div>
        </div>
        <div class="white-bg4">

        </div>

        <div @click="submitFilter()" :class="{clickRed: clickRed}" class="red-button">
            <h1>OK</h1>
            <div v-if="clickRed" class="bg"></div>
        </div>

    </div>
</template>

<script>
import $ from "jquery";

  export default {
    name: 'FilterMenu',
    data(){
      return{
          interval: true,
          currentCalories: 1000,
          clickRed: false,
          filterClose: false,
          promo: false,
          vegan: false, 
          dairyFree: false,
          vegetarian: false,
          halal: false,
          kosher: false,
          glutenFree: false,
          nutFree: false,
          dishKind: 'main'
      }
    },
    props: {
        
    },
    mounted(){
        setTimeout(() => {
            dragElement(document.getElementById(("prods")));
            var rotate = 0
            function dragElement(elmnt) {
                var pos1 = 0, pos2 = 0;

                if (document.getElementById(elmnt.id)) {
                    document.getElementById(elmnt.id).onmousedown = dragMouseDown;
                    elmnt.addEventListener("touchend", dragMouseDown)
                } else {
                    elmnt.onmousedown = dragMouseDown;
                    elmnt.addEventListener("touchstart", dragMouseDown);
                }
                function dragMouseDown(e) {
                    e = e || window.event;
                    if(e.clientX){
                        pos2 = e.clientX
                    }else{
                        pos2 = e.changedTouches[0].clientX;
                    }
                    document.onmouseup = closeDragElement;
                    document.onmouseleave = closeDragElement;
                    elmnt.addEventListener("touchend", closeDragElement)
                    elmnt.addEventListener("touchcancel", closeDragElement)
                    document.onmousemove = elementDrag;
                    elmnt.addEventListener("touchmove", elementDrag)
                }

                function elementDrag(e) {
                    e = e || window.event;
                    console.log(e.changedTouches[0].clientX)
                    console.log(e.touches[0].clientX)

                    if(e.clientX){
                        pos1 = pos2 - e.clientX;
                        pos2 = e.clientX;
                    }else{
                        pos1 = pos2 - e.changedTouches[0].clientX;
                        pos2 = e.changedTouches[0].clientX;
                    }
                    console.log(pos1)
                    console.log(rotate)
                    if(pos1 > 0){
                        if(rotate > -45){
                            rotate -= 3/2
                        }
                    }else{
                        if(rotate < 45){
                            rotate +=3/2
                        }
                    }
                    console.log(rotate)
                    elmnt.style.transform = "rotate(" + rotate + "deg)"

                    for(let i = 0; i <= 8; i++){
                        let newRotate = 0
                        let name = 'promo'
                        switch (i) {
                            case 8:
                                name = 'promo'
                                break;
                            case 7:
                                name = 'vegan'
                                break;
                            case 6:
                                name = 'dairy-free'
                                break;
                            case 5:
                                name = 'vegetarian'
                                break;
                            case 4:
                                name = 'halal'
                                break;
                            case 3:
                                name = 'kosher'
                                break;
                            case 2:
                                name = 'gluten-free'
                                break;
                            case 1:
                                name = 'nut-free'
                                break;
                            default:
                                break;
                        }
                        newRotate = - (i - 1) * 26 + 1 - rotate
                        
                        
                        document.getElementById(elmnt.id + name).style.transform = "rotate(" + newRotate + "deg)"
                    }
                }

                function closeDragElement() {
                    document.onmouseup = null;
                    document.onmousemove = null;
                    document.touchmove = null;
                    document.onmouseleave = null;
                    document.touchend = null;
                    document.touchcancel = null;
                }
            }
        }, 1000);
    },
    methods:{
        submitFilter(){
            this.clickRed = true
            setTimeout(() =>{
                this.filterClose = true
                this.$emit('close')
                setTimeout(() => {
                    this.clickRed = false
                }, 1200);
            }, 1200)
            
        }
    },

  }
  
</script>

<style lang="scss" scoped>
.background{
    z-index: 100;
    position: fixed;
    left: 0;
    top: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0, 0, 0, 0.3);
    pointer-events: none;
}
.white-bg1{
    z-index: 103;
    width: 174vw;
    height: 174vw;
    border-radius: 85%;
    position: absolute;
    left: -8vw;
    bottom: calc(1px - (33vh + 100vw/6));
    background: white;
    display: flex;
    justify-content: center;
    h1{
        @include fontMontserrat(12px, 600, 16px);
        color: $color-strong-grey;
        text-transform: uppercase;
    }
    .kind-dish{
        position: absolute;
        top: -75px;
        display: flex;
        .circle{
            height: 55px;
            border-radius: 50%;
            width: 55px;
            background: white;
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0 22px;
            text-transform: uppercase;
            &:after{
                content: attr(data-circle);
                position: absolute;
                top: calc(100% + 10px);
                color: white;
                @include fontMontserrat(10px, 600, 15px);
                white-space: nowrap;
            }
            img{
                filter: invert(1);
            }
            
        }
        .main{
            transform: translateY(-25px);
            
        }
        .active{
            background: $color-light-red;
            img{
                filter: invert(0);
            }
        }
    }
}

.white-bg2{
    z-index: 104;
    width: 132vw;
    height: 132vw;
    border-radius: 50%;
    position: absolute;
    left: 12vw;
    bottom: calc(1px - (20vh + 100vw/6));
    background: white;
    border: 1px solid #C8C8C8;
    display: flex;
    justify-content: center;
    .container{
        z-index: 9999999;
        margin-top: 220px;
        transform: rotate(0deg);
        display: flex;
        margin-bottom: -20px;
        margin-right: calc(-10px + (110% - 10vh));
        -moz-user-select: none;
        -khtml-user-select: none;
        user-select: none; 
        .block {
            width: 240px;
            height: 50px;
            transform-origin: 100% 26px;
            transform: rotate(180deg);
            position: absolute;
            .square {
                width: calc(55px + 1vw);
                height: calc(55px + 1vw);
                border-radius: 50%;
                display: flex;
                justify-content: center;
                align-items: center;  
                img{
                    width: 45px;
                }
                p{
                    position: absolute;
                    margin: 0;
                    font-size: 10px;
                    top: 60px;
                    text-transform: uppercase;
                }
            }
            .active{
                color: $color-light-red;
            }
        }

        @for $i from 1 through 8 {
            .block:nth-child(#{$i}) { 
                .square{
                    transform: rotate(-(180deg - ($i - 1) * 26deg  - 13deg + 14deg));
                }
                animation: rot#{$i} both ease-in-out;
                animation-duration: 1000ms ; 
            }
        
            @keyframes rot#{$i} {
                0%{
                    transform: rotate(180deg);
                }
                100%{
                    transform: rotate((180deg - ($i - 1) * 26deg  - 13deg) + 14deg);
                }
            }
        } 
    }

}

.white-bg3{
    z-index: 105;
    width: 113vw;
    height: 125vw;
    border-radius: 50%;
    position: absolute;
    left: 22vw;
    bottom: calc(1px - (32vh + 100vw/6));
    background: white;
    border: 1px solid #C8C8C8;
    .container{
        z-index: 9999999;
        margin-top: 195px;
        transform: rotate(0deg);
        margin-right: -25%;
        margin-bottom: -20%;
        margin-left: calc(4vw - 25px + (100vw - 375px)/2);
        .block {
            width: 220px;
            height: 50px;
            transform-origin: 100% 26px;
            transform: rotate(180deg);
            position: absolute;
            .calories {
                width: calc(80px + 1vw);
                height: calc(80px + 1vw);
                border-radius: 50%;
                display: flex;
                justify-content: center;
                align-items: center;  
                margin-bottom: -50px;
                p{  
                    margin: 0;
                    text-transform: uppercase;
                    margin-bottom: calc(33px);
                }
            }
            .active {
                width: calc(80px + 1vw);
                height: calc(80px + 1vw);
                border-radius: 50%;
                display: flex;
                justify-content: center;
                align-items: center;  
                p{  
                    @include fontMontserrat(18px, 600, 24px);
                    color: #3A3A3A;
                    margin: 0;
                    text-transform: uppercase;
                    margin-bottom: calc(33px);
                }
            }
        }

        @for $i from 1 through 8 {
            .block:nth-child(#{$i}) { 
                .calories{
                    p{
                        transform: rotate(-90deg);
                    }
                }
                animation: rot2#{$i} both ease-in-out;
                animation-duration: 1100ms ; 
            }
        
            @keyframes rot2#{$i} {
            0%{
                transform: rotate(0deg);
                }
                100%{
                transform: rotate((90deg + ($i - 4) * 22deg ) );
                }
            }
        } 
    }

}
.white-bg4{
    z-index: 106;
    width: 66vw;
    height: 71vw;
    border-radius: 50%;
    position: absolute;
    left: 45vw;
    bottom: calc(1px - (15vh + 100vw/5));
    background: white;
    border: 1px solid #C8C8C8;
    &::after{
        content: '';
        background: $color-red;
        height: 10px;
        width: 10px;
        border-radius: 50%;
        position: absolute;
        top: -5px;
        left: calc(50% - 5px);

    }
    &::before{
        content: 'CALORIES';
        @include fontMontserrat (9px, bold, 12px);
        color: $color-strong-grey;
        position: absolute;
        top: -20px;
        left: calc(50%);
        transform: translateX(-50%);

    }
}


.red-button{
    z-index: 107;
    position: absolute;
    height: 40vw;
    width: 40vw;
    border-radius: 50%;
    background: $color-red;
    bottom: 0;
    left: 58vw;
    bottom: calc(1px - (6vh + 100vw/5));
    display: flex;
    justify-content: center;
    h1{
        font-family:'Comfortaa',sans-serif;
        font-style: normal;
        font-weight: bold;
        font-size: 16px;
        line-height: 18px;
        color: #FFFFFF;

    }
}
.clickRed{
    animation: clickRed 2.5s forwards ease-in-out;
    .bg{
        position: fixed;
        left: 0;
        top: 0;
        width: 100vw;
        height: 100vh;
        background: url(../assets/bg.svg);
        animation: animBg .5s .8s forwards ease-in-out;
        filter: opacity(0);
    }
}


@keyframes clickRed {
    0%{
        height: 40vw;
        width: 40vw;
        left: 58vw;
    }
    67%{
        height: 400vw;
        width: 400vw;
        left: -118vw;
    }
    100%{
        height: 400vw;
        width: 400vw;
        left: -118vw;
    }
}

@keyframes animBg {
    0%{
        filter: opacity(0);
    }
    100%{
        filter: opacity(1);
    }
}

</style>
