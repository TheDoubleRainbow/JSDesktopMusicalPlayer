var Vue = require('./vue.js');
var glob = require('glob');
var id3 = require('id3js');

new Vue({
	el: "#main",
	data: {
		tracks: [],
		currentTrack: {},
		player: {
			volume: 1
		}
	},
	created: function(){
		this.getTracks()
	},
	methods: {
		setTrack: function(track){
			this.currentTrack = track;
			setTimeout(function(){document.getElementById("music").play()}, 1000)
			music.paused = false;
		},
		getTracks: function(){
			let that = this;
			this.tracks = [];
			glob("music/*.mp3", function (er, files) { //Searching for files
				id3({ file: files[0], type: id3.OPEN_LOCAL }, function(err, tags) { // getting id3 tags from mp3
    					that.currentTrack = {name: tags.artist + ' - ' + tags.title, genre: tags.v1.genre, way: files[0]};

				});
				files.forEach(function(file){
					id3({ file: file, type: id3.OPEN_LOCAL }, function(err, tags) {
    					that.tracks.push({name: (tags.artist + ' - ' + tags.title), genre: tags.v1.genre, way: file})
					});
				})
			})
		},
	}
})

require('./audioControls.js'); //player controls