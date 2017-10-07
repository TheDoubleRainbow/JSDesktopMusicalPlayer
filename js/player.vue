var Vue = require('./vue.js');
new Vue({
	el: "#main",
	data: {
		tracks: ["New Pirate.mp3, Russian rock.mp3, Lolita.mp3"],
		currentTrack: {name: "New Pirate.mp3", pic: "../pic/track.jpg"},
	},
	create: function(){
	}
})