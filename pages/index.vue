<template>
  <div>
    <v-dialog v-model="dialog" width="500">
      <template v-slot:activator="{ on, attrs }">
        <v-card class="mx-auto" color="colors.orange.lighten5">
          <v-container>
            <v-row dense justify="center" align="center">
              <F3Logo class="py-10" />
              <v-col cols="12">
                <v-card color="primary" dark>
                  <v-card-title class="text-h5"> クイズを主催する </v-card-title>

                  <v-card-subtitle>
                    クイズを主催します。&nbsp主催者のみこちらを押してください。
                  </v-card-subtitle>

                  <v-card-actions>
                    <v-btn text nuxt to="/host"> 開始 </v-btn>
                  </v-card-actions>
                </v-card>
              </v-col>
              <v-col cols="12">
                <v-card color="secondary" dark>
                  <v-card-title class="text-h5"> クイズに参加する </v-card-title>

                  <v-card-subtitle
                    >他の人が開始したクイズに参加します。&nbsp参加にはルームIDが必要です。</v-card-subtitle
                  >

                  <v-card-actions>
                    <v-btn text v-bind="attrs" v-on="on"> 参加する </v-btn>
                  </v-card-actions>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">参加情報</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  label="ルームID"
                  v-model="$v.form.clientRoomId.$model"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  label="参加者名"
                  v-model="$v.form.clientName.$model"
                  counter="10"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="dialog = false"> キャンセル </v-btn>
          <v-btn color="blue darken-1" text @click="enterClient()"> 入室 </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import HostBtn from "../components/HostBtn.vue";
import F3Logo from "../components/F3Logo.vue";
import ClientBtn from "../components/ClientBtn.vue";
import EntryModal from "../components/EntryModal.vue";
import { required, alphaNum, maxLength, minLength } from "vuelidate/lib/validators";
export default {
  head() {
    return {
      title: "TOP",
    };
  },
  name: "IndexPage",
  data() {
    return {
      dialog: false,
      form: {
        clientName: "",
        clientRoomId: "",
        check: false,
      },
    };
  },
  components: { HostBtn, F3Logo, ClientBtn, EntryModal },
  methods: {
    enterClient() {
      if (this.$v.$invalid) {
        alert("入力に誤りがあります");
      } else if (false) {
        alert("ルームIDが正しくありません");
      } else {
        this.$router.push({
          path: "client",
          query: { name: this.form.clientName, roomId: this.form.clientRoomId },
        });
      }
    },
  },
  validations: {
    form: {
      clientName: {
        required,
        maxLength: maxLength(10),
      },
      clientRoomId: {
        required,
        alphaNum,
        maxLength: maxLength(8),
        minLength: minLength(8),
      },
      check: {},
    },
  },
};
</script>
