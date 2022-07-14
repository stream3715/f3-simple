<template>
  <v-container full-height>
    <v-dialog v-model="dialog" width="500">
      <template #activator="formActivator">
        <v-container>
          <v-row dense justify="center" align="center">
            <!-- <F3Logo class="py-10" /> -->
            <v-col cols="12">
              <v-card color="primary" dark>
                <v-card-title class="text-h5"> クイズを主催する </v-card-title>

                <v-card-subtitle>
                  クイズを主催します。主催者のみこちらを押してください。
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
                  >他の人が開始したクイズに参加します。参加にはルームIDが必要です。</v-card-subtitle
                >

                <v-card-actions>
                  <v-btn
                    text
                    v-bind="formActivator.attrs"
                    v-on="{ ...formActivator.on }"
                  >
                    参加する
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
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
                  v-model="$v.form.clientRoomId.$model"
                  label="ルームID"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  v-model="$v.form.clientName.$model"
                  label="参加者名"
                  counter="10"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="dialog = false">
            キャンセル
          </v-btn>
          <v-btn color="blue darken-1" text @click="enterClient()">
            入室
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import {
  required,
  alphaNum,
  maxLength,
  minLength,
} from 'vuelidate/lib/validators'
export default {
  name: 'IndexPage',
  components: {},
  data() {
    return {
      dialog: false,
      form: {
        clientName: '',
        clientRoomId: '',
        check: false,
      },
    }
  },
  head() {
    return {
      title: 'TOP',
    }
  },
  methods: {
    enterClient() {
      if (this.$v.$invalid) {
        alert('入力に誤りがあります')
      } else {
        this.$router.push({
          path: 'client',
          query: { name: this.form.clientName, roomId: this.form.clientRoomId },
        })
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
}
</script>
