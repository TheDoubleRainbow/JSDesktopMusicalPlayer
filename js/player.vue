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
    created: function() {
        this.getTracks()
    },
    methods: {
        setTrack: function(track) {
            if (track == "next") {
                if (this.tracks[this.tracks.indexOf(this.currentTrack) + 1]) {
                	console.log(this.tracks[this.tracks.indexOf(this.currentTrack) + 1])
                    this.currentTrack = this.tracks[this.tracks.indexOf(this.currentTrack) + 1];
                    setTimeout(function() { document.getElementById("music").play() }, 1000)
                } else {
                    console.log("Next track does not exist")
                }
            } else {
                this.currentTrack = track;
                setTimeout(function() { document.getElementById("music").play() }, 1000)
                music.paused = false;
            }
        },
        getTracks: function() {
            let that = this;
            this.tracks = [];
            glob("music/*.mp3", function(er, files) {
                files.forEach(function(file) {
                    id3({ file: file, type: id3.OPEN_LOCAL }, function(err, tags) {
                        that.tracks.push({ name: (tags.artist + ' - ' + tags.title), genre: tags.v1.genre, way: file })
                    });
                })
                setTimeout(function(){
                	that.currentTrack = that.tracks[0]
                }, 500)
            })
        },
    }
})

require('./audioControls.js'); //player controls