<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">My music</div>

                    <div class="card-body">
                       <h2>{{ current.title }} - <span>{{ current.artist }}</span></h2>
                    </div>
                    <div class="control">
                        <button class="prev" @click="prev">Prev</button>
                        <button class="play" v-if="!isPlaying" @click="play">Play</button>
                        <button class="pause" v-else @click="pause">Pause</button>
                        <button class="next" @click="next">Next</button>
                    </div>

                    <section class="playlist">
                        <h3>The Playlist</h3>
                        <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">
                            {{ song.title }} - {{ song.artist }}
                        </button>
                    </section>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                current: {},
                index:0,
                isPlaying: false,

                songs: [
                    {
                        title: 'BANKS You Should Know Where Im Coming From (Cartoon Bootleg)',
                        artist:'BANKS',
                        src:'audio/BANKS You Should Know Where Im Coming From (Cartoon Bootleg).mp3'
                    },
                    {
                        title: 'Halcyon',
                        artist:'Hybrid Minds',
                        src: 'audio/Halcyon (feat. Grimm).mp3'
                    }
                ],

                player: new Audio()
            }
        },

        created() {
            this.current = this.songs[this.index]
            this.player.src = this.current.src
        },

        methods: {
            play(song) {
                if(typeof song.src != "undefined") {
                    this.current = song;

                    this.player.src = this.current.src
                }

                this.player.play();
                this.isPlaying = true
            },

            pause() {
                this.player.pause()
                this.isPlaying = false
            },

            next() {
                this.index++
                if (this.index > this.songs.length - 1) {
                    this.index = 0;
                }

                this.current = this.songs[this.index];
                this.play(this.current)
            },
           
            prev() {
                this.index--
                if (this.index < 0) {
                    this.index = this.songs.length - 1;
                }

                this.current = this.songs[this.index];
                this.play(this.current)
            }


        }
    }
</script>
