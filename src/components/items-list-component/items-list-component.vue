<template>
  <ul class="item-list">
    <li
      class="item-list--item"
      v-for="(transcription, index) in transcriptionList"
      v-bind:key="index"
      :tabindex="index + 2"
    >
      <div class="delete-icon">
        <button
          aria-pressed="false"
          role="button"
          class="delete-button"
          @click="deleteRow(transcription.id)"
        >
          <svgicon
            class="person-icon"
            name="delete"
            height="1.2rem"
            width="1.2rem"
            :original="true"
          ></svgicon>
        </button>
      </div>
      <div>
        <label class="checkbox-container">
          <input type="checkbox" />
          <span class="checkmark" />
        </label>
        <figure>
          <svgicon
            class="person-icon"
            name="person"
            height="1.5rem"
            width="1.5rem"
            :original="true"
          ></svgicon>
        </figure>
      </div>
      <InplaceEditor
        v-bind:transcriptionInfo="{voice: transcription.voice, text: transcription.text, id: transcription.id}"
      />
    </li>
  </ul>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import { State, Action } from 'vuex-class';
import InplaceEditor from '@/components/Inplace-editor-component/Inplace-editor-component.vue';
import SvgIcon from 'vue-svgicon';
import '../icons/delete';
import '../icons/person';
import { ITranscription } from '../../store/types';

const namespace: string = 'transcription';

@Component({
  components: {
    svgicon: SvgIcon,
    InplaceEditor
  }
})
export default class ItemsList extends Vue {
  @Prop() private transcriptionList!: ITranscription[];
  @Action('deleteTranscription', { namespace })
  private deleteTranscription: any;
  private previousTabIndex: number = 0;

  private deleteRow(rowId: number) {
    this.deleteTranscription(rowId);
  }
}
</script>

