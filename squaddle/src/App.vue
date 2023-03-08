<template>
  <v-app class="squaddle">
    <v-main>
      <v-tabs class="bg-primary-dark text-white" grow color="secondary">
        <v-tab title="Schedule"></v-tab>
        <v-tab title="Squad"></v-tab>
        <v-tab title="Payments"></v-tab>
      </v-tabs>

      <v-card-text>
        <v-window v-model="tab">
          <v-window-item value="schedule">
            <div class="pa-3" v-if="mode === 'default'">
              <div class="d-flex justify-space-between">
                <div class="text-h6 font-weight-bold text-primary-dark">Tuesday football</div>
                <v-icon icon="mdi-dots-vertical"></v-icon>
              </div>
              <div class="py-2">
                <div class="my-3">
                  <v-icon icon="mdi-calendar-blank" color="primary"></v-icon>
                  <span class="ml-2 text-primary font-weight-medium">Tuesday, 22 September 2022</span>
                </div>
                <div class="my-3">
                  <v-icon icon="mdi-clock" color="primary"></v-icon>
                  <span class="ml-2 text-primary font-weight-medium">21:00-22:00</span>
                </div>
                <div class="my-3">
                  <v-icon icon="mdi-map-marker" color="primary"></v-icon>
                  <span class="ml-2 text-primary font-weight-medium">Hackney City Academy</span>
                </div>
                <div class="my-3">
                  <v-icon icon="mdi-account-multiple" color="primary"></v-icon>
                  <span class="ml-2 text-primary font-weight-medium">Min 12/16 Max</span>
                </div>
                <div class="my-3">
                  <v-icon icon="mdi-currency-gbp" color="primary"></v-icon>
                  <span class="ml-2 text-primary font-weight-medium">5</span>
                </div>
              </div>
              <div class="my-3">
                <v-btn color="primary" prepend-icon="mdi-message-text"  size="large" block>
                  Send message
                </v-btn>
              </div>
              <div class="my-3">
                <v-btn @click="mode = 'teamNames'" color="secondary" prepend-icon="mdi-account-multiple"
                       size="large" block>
                  Team selector
                </v-btn>
              </div>
            </div>
            <div class="pa-3" v-if="mode === 'teamNames'">
              <div class="text-h6 mb-5 font-weight-bold text-primary-dark">Team names</div>
              <div class="mb-4">Enter a name for each team.</div>

              <div class="d-flex">
                <v-text-field v-model="teamA" placeholder="Team 1" variant="outlined"
                              class="rounded-pill mr-2 border-primary"></v-text-field>
                <v-text-field v-model="teamB" placeholder="Team 2" variant="outlined"
                              class="rounded-pill ml-2"></v-text-field>
              </div>
              <span class="text-primary-dark">E.g. Darks and Lights; Blues and Reds; or Starters and Subs if you play in a league.</span>

              <div class="d-flex mt-10 justify-space-between">
                <v-btn color="primary" variant="text" @click="mode = 'default'">Back</v-btn>
                <v-btn color="primary"  @click="mode = 'addPlayers'">Next</v-btn>
              </div>
            </div>

            <div class="pa-3" v-if="mode === 'addPlayers'">
              <div class="text-h6 mb-5 font-weight-bold text-primary-dark">Select Teams</div>
              <div class="mb-4">Add participants to each team.</div>

              <div class="d-flex">
                <span class="text-h6 w-50">{{ teamA }}</span>
                <span class="text-h6">{{ teamB }}</span>
              </div>

              <div class="d-flex">
                <span class="w-50 pr-5">
                  <ol class="px-2">
                    <li class="my-5 text-primary" v-for="player in teamAPlayers">
                      <div class="d-flex justify-space-between align-content-center mx-3">
                        <span>                      {{ player }}                        </span>
                        <v-btn icon="mdi-close" flat size="sm" @click="teamAPlayers = teamAPlayers.filter(p => p !== player)" />
                        </div>
                    </li>
                  </ol>
                  <v-select v-model="teamAPlayers" color="primary" menu-icon="false" :items="teamAOptions"
                            placeholder="Add player"
                            multiple
                            hide-selected
                            persistent-placeholder
                            prepend-inner-icon="mdi-plus">
                    <template #selection>

                    </template>
                  </v-select>

                </span>
                <span class="w-50">
                    <ol class="px-2">
                    <li class="my-5 text-primary" v-for="player in teamBPlayers">
                      <div class="d-flex justify-space-between align-content-center mx-3">
                        <span>                      {{ player }}                        </span>
                        <v-btn icon="mdi-close" flat size="sm"
                               @click="teamBPlayers = teamBPlayers.filter(p => p !== player)" />
                        </div>
                    </li>
                  </ol>
                  <v-select v-model="teamBPlayers" color="primary" menu-icon="false" :items="teamBOptions"
                            placeholder="Add player"
                            multiple
                            hide-selected
                            persistent-placeholder
                            prepend-inner-icon="mdi-plus">
                    <template #selection>

                    </template>
                  </v-select>

                </span>
              </div>


              <div class="d-flex mt-10 justify-space-between">
                <v-btn color="primary" variant="text" @click="mode = 'teamNames'">Back</v-btn>
                <v-btn color="primary" >Next</v-btn>
              </div>
            </div>
          </v-window-item>

          <v-window-item value="two">
            Two
          </v-window-item>

          <v-window-item value="three">
            Three
          </v-window-item>
        </v-window>
      </v-card-text>


    </v-main>
  </v-app>
</template>

<script setup lang="ts">
import { computed, ref } from "vue";

const tab = ref("schedule")
const mode = ref("default");
const teamA = ref("Team 1")
const teamB = ref("Team 2")

const teamAPlayers = ref<string[]>([]);
const teamBPlayers = ref<string[]>([]);
const players = ref([
  "Barry Cresswell",
  "Tony Maloney",
  "Mark Quark",
  "Richard Pritchard",
  "Ron Gammon",
  "Mandy Sanderson",
  "Terrance Penance",
  "Michael Pike",
  "Cindy Plinth",
  "Jamie Andrews",
  "Scott Scrivens",
  "Ian Kilbourn",
  "Adam Borowski",
  "Ricky Cheng",
  "Alex Bexon",
  "Ryan Roulette",
])

const teamAOptions = computed(() => {
  return players.value.filter(p => !teamBPlayers.value.includes(p))
})

const teamBOptions = computed(() => {
  return players.value.filter(p => !teamAPlayers.value.includes(p))
})

</script>

<style lang="scss">
.squaddle {
  .v-field__prepend-inner {
    .mdi {
      color: #5252C1;
    }
  }

  .v-field__input {
    opacity: 1;


    input {
      color: #5252C1;
      opacity: 1;
      font-weight: bold
    }
  }
}
</style>
