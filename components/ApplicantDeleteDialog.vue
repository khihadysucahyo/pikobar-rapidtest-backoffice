<template>
  <div>
    <v-dialog :value="open" max-width="528">
      <v-card class="text-center">
        <v-card-title>
          <span class="col pl-10">Perhatian!</span>
        </v-card-title>
        <v-card-text>
          <div>
            {{ confirmDeleteMsg }}
          </div>
          <span>Nama peserta: </span>
          <strong v-if="dialogType === 'applicant'">
            {{ record ? record.name : '-' }}
          </strong>
          <strong v-else>
            {{ record ? record.applicant.name : '-' }}
          </strong>
        </v-card-text>
        <v-card-actions class="pb-6 justify-center">
          <v-btn
            color="grey darken-1"
            outlined
            class="mr-2 px-2"
            @click="close"
          >
            Tidak
          </v-btn>
          <v-btn color="error" class="ml-2 px-2" @click="remove">
            Ya
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
import { CONFIRM_DELETE_PARTICIPANTS } from '@/utilities/constant'
export default {
  props: {
    open: {
      type: Boolean,
      default: false
    },
    record: {
      type: Object,
      default: null
    },
    dialogType: {
      type: String,
      default: 'applicant'
    }
  },
  data() {
    return {
      confirmDeleteMsg: CONFIRM_DELETE_PARTICIPANTS
    }
  },
  methods: {
    close() {
      this.$emit('close')
    },
    remove() {
      this.$emit('remove', this.record)
    }
  }
}
</script>
