<template>
  <div class="hello">

    <h1> Mariage de {{ msg }} </h1>

    <div>
      <video ref="video" id="video" width="640" height="480" autoplay v-on:click="capture()"></video>
    </div>

    <div>
      <textarea id="textarea_message" placeholder="Votre message pour les mariés..." required></textarea>
    </div>
    <div>
      <input type="text" id="text_name" name="text_name" required minlength="4" maxlength="20" placeholder="Votre nom" />	
      <input type="tel" id="text_number" name="text_number" pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}" placeholder="Votre numéro de téléphone" />
    </div>
    <div>
      <button v-on:click="sendPicture()">Envoyer ma photo !</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'JoinParty',
  props: {
    msg: String
  },
data() {
            return {
                video: {},
                canvas: {},
                captures: []
            }
        },
  mounted() {
            this.video = this.$refs.video;
            if(navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
                navigator.mediaDevices.getUserMedia({ video: true }).then(stream => {
                      this.video.srcObject = stream
                      var playPromise = this.video.play()

                      if (playPromise !== undefined) {
                        playPromise.then({
                          // Automatic playback started!
                          // Show playing UI.
                        })
                        .catch(error => {
                          throw new Error(error)
                          // Auto-play was prevented
                          // Show paused UI.
                          });
                        }
                  });
              }
    },
  methods: { 
    capture() {
      if (!this.video.paused){
        this.video.pause();
      } else {
        this.video.play();  
      }
    },
    sendPicture() {
        var obj = new Object();
        obj.message = no.val();
        obj.image  = canvas.toDataURL('image/jpeg');
        obj.numberSender = $('#text_number').val();
        obj.nameSender = $('#text_name').val();
        obj.idPublic = $('#publicId').val();
        var jsonString= JSON.stringify(obj);
        
        this.axios.post('http://localhost:8000/yourPostApi', {
                    name: this.name,
                    description: this.description
                })
                .then(function (response) {
                    currentObj.output = response.data;
                })
                .catch(function (error) {
                    currentObj.output = error;
                });
        
        $.ajax({
          type: 'POST',
            url: 'http://localhost:8080/message',
            contentType: "application/json; charset=utf-8",
            dataType: "json",
            context: document.body,
            data: jsonString,
            success: function(){
              alert('OK');
            }
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
    body {
        background-color: #F0F0F0;
    }
    #app {
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
    #video {
        background-color: #000000;
    }
</style>
