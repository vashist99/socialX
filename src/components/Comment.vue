<template>
  <v-container fluid grid-list-md pa-1>
    <v-layout row wrap>
      <v-flex xs2 sm1>
        <!-- <router-link :to="{  name: 'Profile', params: {username}}"> -->
        <v-avatar>
          <v-img :src="photo"></v-img>
        </v-avatar>
        <!-- </router-link> -->
      </v-flex>
      <v-flex xs10 sm11>
        <v-layout row wrap>
          <v-flex>
            <v-layout row wrap>
              <v-flex xs10>
                <strong>{{ name}}</strong>
              </v-flex>
              <v-flex xs2 class="text-xs-right">
                <small>{{comment.created| moment("from") }}</small>
              </v-flex>
              <v-flex xs12>
                <template>
                  <p
                    style="overflow-wrap: break-word"
                    v-for="(line,i) in comment.content.split('\n')"
                    :key="i"
                  >{{line}}</p>
                </template>
              </v-flex>
            </v-layout>
          </v-flex>
        </v-layout>
      </v-flex>
    </v-layout>
    <!-- <v-divider v-if="count != pr+1"></v-divider> -->
  </v-container>
</template>

<script>
import axios from "axios";
import qs from "qs";

export default {
  name: "Comment",
  props: ["comment", "pr", "count"],
  data() {
    return {
      name: "",
      photo:
        "https://avataaars.io/?avatarStyle=Transparent&topType=ShortHairShortCurly&accessoriesType=Prescription02&hairColor=Black&facialHairType=Blank&clotheType=Hoodie&clotheColor=White&eyeType=Default&eyebrowType=DefaultNatural&mouthType=Default&skinColor=Light",
      username: "",
      lorem:
        "Lorem ipsum dolor sit amet, mel at clita quando. Te sit oratio vituperatoribus, nam ad ipsum posidonium mediocritatem, explicari dissentiunt cu mea. Repudiare disputationi vim in, mollis iriure nec cu, alienum argumentum ius ad. Pri eu justo aeque torquatos."
    };
  },
  created() {
    axios.get("/users/" + this.comment.postedBy).then(res => {
      this.name = res.data.name;
    });
    this.username = this.comment.postedby;
  }
};
</script>

<style scopped>
.shiftcomment {
  padding-left: 10%;
}
p {
  margin: 0;
}
</style>