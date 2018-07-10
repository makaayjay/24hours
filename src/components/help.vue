<template>
          <div class="cover"  v-if="isLogShow"  >
            <div  class="cover2"  @click="closeSelf"></div>
          <transition name="drop">
          <div class="dialog"  v-if="isLogShow">
            <h1>简介：</h1><span @click="closeSelf">X</span>
            <hr>
            <p>&nbsp;&nbsp;&nbsp;&nbsp;北京市城市街区24小时自助图书馆建设项目，是在北京市文化局的指导下，由首都图书馆牵头各区县图书馆共同实施建设，是北京市文化系统的折子工程。它基于北京市公共图书馆计算机信息服务网络，突破了时间、地点等因素的制约，将公共图书馆服务送入街区，市民可就近享受借书、还书、申办读者证等免费服务，成为公共图书馆服务体系的重要组成部分。</p>
            <h1>功能：</h1>
            <hr>
            <p >1、申办读者卡 </p>
            <p >&nbsp;&nbsp;&nbsp;&nbsp;市民可凭二代身份证在自助图书馆服务机上申办读者卡。(目前自助图书馆服务机只限办理具有普通中文文献外借功能的读者证，办证时需缴纳借书押金为100元，存入押金时，只能接收50及100元面值人民币，不设找赎。当读者需要退证时，应归还所有外借文献资料，由读者本人携带读者证、身份证件原件，前往首都图书馆现场办理。如代办，则还需提供代办人的身份证原件。若读者证丢失后办理退证，须本人亲自办理，不可代办。读者证若不慎遗失，请及时到首都图书馆办证处或通过电话办理挂失。补证须本人亲自到首都图书馆现场办理，不可代办。补证收费2元。 )</p>
            <p >2、自助借还书 </p>
            <p >&nbsp;&nbsp;&nbsp;&nbsp;持含外借功能读者卡的读者，可在任意一台自助图书馆服务机上借阅文献，也可将自助图书馆所借图书归还到任意一个自助图书馆服务机上。读者可在任意一台自助图书馆服务机上借还文献，可外借文献数量与外借周期与馆内外借相同。 </p>
            <p >3、续借服务 </p>
            <p >&nbsp;&nbsp;&nbsp;&nbsp;读者可在自助图书馆服务机上办理图书或光盘的续借手续。通过自助图书馆系统办理图书或光盘续借时，可一次性续借所有图书或光盘，只能续借1次。 </p>
            <p >4、查询服务 </p>
            <p >&nbsp;&nbsp;&nbsp;&nbsp;读者可通过自助图书馆查询机访问&#8220;北京市公共图书馆计算机信息服务网&#8221;(<a href="http://www.bplisn.net.cn/" >http://www.bplisn.net.cn/</a>)，查询图书馆信息和馆藏状况。自助服务机的屏幕可实时显示本机的文献情况。 </p>
            <p >5、读者卡透支 </p>
            <p >&nbsp;&nbsp;&nbsp;&nbsp;读者在自助图书馆服务机上办理图书归还时，如出现逾期费，系统会自动提示当前的支付方式为透支操作，必须由读者点击确认。每张读者卡的最高透支金额为10元，如透支金额超过10元，读者卡将会暂停服务。读者卡出现透支情况后，读者需携带本人读者卡到最初办卡的&#8220;一卡通&#8221;联网图书馆办理透支金额补交手续，每次补交透支金额时需一次性全部补交。逾期费标准依图书资产所属各联网馆的相关规定执行。 </p>
          </div>
          </transition>
          </div>
</template>

<script>
    export default {
      name: "help",
      props:{
        isLogShow:{
          default:false,
        }
      },
      methods:{
        closeSelf(){
          this.$emit('closeDialog')
        }
      },
    }
</script>

<style scoped>

.cover{
  position: fixed;
  width: 100%;
  height: 100%;
  z-index: 4;
}
.cover2{
  z-index: 5;
  width: 100%;
  height: 100%;
  background: rgba(52,52,52,0.5);
}
  .dialog{
    width: 60%;
    height: 500px;
    background: white;
    position: fixed;
    top: 50px;
    left: 15%;
    padding: 20px 10px;
    border-radius: 8px;
    overflow-y: scroll;
    z-index: 60;
  }
.dialog h1{
  text-align: left;
  font-weight: bold;
  font-size: 20px;
}
.dialog span{
  cursor: pointer;
  position: absolute;
  right: 10px;
  top: 10px;
  display: inline-block;
  width: 30px;
  height: 30px;
  line-height: 30px;
  color: red;
  border: 1px solid #efefef;
}
.dialog p{
  text-align: left;
  line-height: 30px;
}
  .drop-enter-active {
    transition: all .5s ease;
  }
  .drop-leave-active {
    transition: all .3s ease;
  }
  .drop-enter {
    transform: translateY(-500px);
  }
  .drop-leave-active {
    transform: translateY(-500px);
  }
</style>
