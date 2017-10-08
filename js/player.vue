var Vue = require('./vue.js');
var glob = require('glob');
var id3 = require('id3js');

new Vue({
	el: "#main",
	data: {
		tracks: [],
		currentTrack: {},
		player: {
			html: document.querySelector('#player'),
			state: false,
		}
	},
	created: function(){
		this.getTracks(true)
	},
	methods: {
		setTrack: function(id){
			console.log(this.tracks)
		},
		getTracks: function(){
			let that = this;
			this.tracks = [];
			glob("music/*.mp3", function (er, files) {
				id3({ file: files[0], type: id3.OPEN_LOCAL }, function(err, tags) {
    					that.currentTrack = {name: tags.artist + ' - ' + tags.title, genre: tags.v1.genre, way: files[0]};
				});
				files.forEach(function(file){
					id3({ file: file, type: id3.OPEN_LOCAL }, function(err, tags) {
    					that.tracks.push({name: tags.artist + ' - ' + tags.title, genre: tags.v1.genre, way: file})
					});
				})
			})
		},
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