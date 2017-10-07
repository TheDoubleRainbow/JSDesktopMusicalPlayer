var Vue = require('./vue.js');
new Vue({
	el: "#main",
	data: {
		tracks: ["New Pirate.mp3, Russian rock.mp3, Lolita.mp3"],
		currentTrack: {name: "Suicide Is Painless", pic: "../pic/track.jpg"},
		player: {
			html: document.querySelector('#player'),
			state: false,
		}
	},
	methods: {
		play: function(){
			if(this.player.state){
				this.player.html.pause();
				this.player.state = false;
			}
			else{
				this.player.html.play()
				this.player.state = true;
			}
		}
	}
})