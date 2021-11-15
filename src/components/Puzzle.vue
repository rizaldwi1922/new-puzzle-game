<template>
<div>
    <button class="btn btn-primary" v-on:click="acak">Mulai ulang</button>
    <h3>
        Cari gambar ini
    </h3>
        <img v-bind:src="require('../assets/images/'+object+'.jpg')" alt="Avatar" style="width:200px;height:200px;">
    <h3>
        Jumlah kesempatan: {{ kesempatan }}
    </h3>
    <div class="row">
        <a href="#" v-for="(item,index) in listGambar" :key="index" v-on:click.prevent="flipCard(index, item)" class="col">
        <div class="flip-card">
            <div class="flip-card-inner" v-bind:id="'card'+index">
                <div class="flip-card-front">
                    <img v-bind:src="require('../assets/images/quest.png')" alt="Avatar" style="width:200px;height:200px;">
                </div>
                <div class="flip-card-back">
                    <img v-bind:src="require('../assets/images/'+item+'.jpg')" alt="Avatar" style="width:200px;height:200px;">
                </div>
            </div>
        </div>
        </a>
        
    </div>

    <div class="modal fade" id="menang" tabindex="-1" role="dialog" aria-hidden="true">
      <div class="modal-dialog modal-dialog-centered" role="document">
      <div class="modal-content">
          <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLongTitle">Selamat !!</h5>
          <button type="button" class="close" v-on:click="closeModalMenang">
              <span aria-hidden="true">&times;</span>
          </button>
          </div>
          <div class="modal-body">
            <p>Anda telah memenangkan permainan</p>
          </div>
      </div>
      </div>
      </div>

      <div class="modal fade" id="kalah" tabindex="-1" role="dialog" aria-hidden="true">
      <div class="modal-dialog modal-dialog-centered" role="document">
      <div class="modal-content">
          <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLongTitle">Coba lagi..</h5>
          <button type="button" class="close" v-on:click="closeModalKalah">
              <span aria-hidden="true">&times;</span>
          </button>
          </div>
          <div class="modal-body">
               <p>Anda gagal memenangkan permainan</p>
          </div>
      </div>
      </div>
      </div>
</div>
</template>

<script>
    export default {
        name: 'Puzzle',
        data:function() {
            return{
                flip: false,
                kesempatan: 5,
                object: '',
                listGambar: []
            }
        },
        methods: {
            flipCard: function(id, value){
                var card = document.getElementById("card" + id);
                if(!this.flip){
                    card.style.transform = "rotateY(180deg)";
                    if(value != this.object){
                        this.kesempatan = this.kesempatan - 1;
                        if(this.kesempatan < 1){
                            this.showModalKalah()
                        }
                    } else {
                        this.showModalMenang()
                    }
                    this.flip = true
                    setTimeout(function(){
                        card.style.removeProperty('transform');
                        this.flip = false
                    }, 3000);
                    
                } else {
                    card.style.removeProperty('transform');
                    this.flip = false
                }
                
            },
            acak: function(){
                this.listGambar = []
                this.kesempatan = 5
                this.object = Math.floor(Math.random() * 5) + 1;
                
                var oneObj = false;
                for(var i = 0;i<10;i++){
                    var generate = Math.floor(Math.random() * 5) + 1;
                    if(!oneObj){
                        if(this.object == generate){
                            oneObj = true
                        }
                        this.listGambar.push(generate)
                    } else {
                        if(this.object != generate){
                            this.listGambar.push(generate)
                        } else {
                            while(this.object == generate){
                                generate = Math.floor(Math.random() * 5) + 1;
                            }
                            this.listGambar.push(generate)
                        }
                    }
                    if(i == 9 && !oneObj) {
                        this.listGambar.push(this.object)
                    }
                }
            },
                showModalMenang: function(){
                    var modal = document.getElementById("menang");
                    modal.classList.add("show");
                    modal.style.display = "block";
                    
                },
                closeModalMenang: function() {
                    var modal = document.getElementById("menang");
                    modal.classList.remove("show");
                    modal.style.display = "none";
                    this.acak()
                },
                showModalKalah: function(){
                    var modal = document.getElementById("kalah");
                    modal.classList.add("show");
                    modal.style.display = "block";
                    
                },
                closeModalKalah: function() {
                    var modal = document.getElementById("kalah");
                    modal.classList.remove("show");
                    modal.style.display = "none";
                    this.acak()
                },
        },
        mounted() {
            this.acak()
            console.log(this.listGambar)
            console.log(this.object)
        },
    }
</script>

<style>
.flip-card {
  background-color: transparent;
  width: 300px;
  height: 200px;
  border: 1px solid #f1f1f1;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}

.flip-card-front {
  background-color: #bbb;
  color: black;
}

.flip-card-back {
  background-color: dodgerblue;
  color: white;
  transform: rotateY(180deg);
}
</style>