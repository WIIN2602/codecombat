<script>
import Modal from '../../common/Modal'
import SecondaryButton from '../common/buttons/SecondaryButton'
import BaseCloudflareVideo from 'app/components/common/BaseCloudflareVideo'

export default Vue.extend({
    components: {
      Modal,
      BaseCloudflareVideo,
      SecondaryButton
    },
    data: () => {
      const videoId = '7897f22d74442c9d41bde91857339382'  // cloudflare id
      return {
        videoId,
        thumbnailUrl: `https://videodelivery.net/${videoId}/thumbnails/thumbnail.jpg?time=1.000s`
      }
    },

    methods: {
      trackEvent(eventName) {
        if (eventName) {
          window.tracker?.trackEvent(eventName, { category: 'Teachers' })
        }
      },
      onClose() {
        this.trackEvent('Welcome Video: Modal Closed')
        this.$emit('close')
      },
      onClickResourceHub () {
        this.trackEvent('Welcome Video: Modal Clicked Resource Hub')
        this.$emit('close')
      }
    }
  })
</script>

<template>
  <modal
    title="Welcome to the new Ozaria Teacher Dashboard"
    @close="onClose"
  >
    <div class="onboarding-video-modal">
      <span class="sub-title"> Watch this brief video for best practices and tips on how to make the most of your dashboard. You can always re-watch it in the <a href="/teachers/resources" @click="onClickResourceHub"> Teacher Toolkit. </a> </span>
      <div class="video">
        <base-cloudflare-video
          :video-cloudflare-id="videoId"
          :thumbnail-url="thumbnailUrl"
          preload="auto"
          @completed="trackEvent('Welcome Video: Completed')"
          @loaded="trackEvent('Welcome Video: Loaded')"
        />
      </div>
      <div class="buttons">
        <secondary-button
          @click="onClose"
        >
          {{ $t("common.next") }}
        </secondary-button>
      </div>
    </div>
  </modal>
</template>

<style lang="scss" scoped>
@import "app/styles/ozaria/_ozaria-style-params.scss";

.onboarding-video-modal {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 20px;
  width: 800px;
}

.sub-title {
  @include font-p-2-paragraph-medium-gray;
}

.video {
  width: 100%;
  padding: 20px 0px;
}

.buttons {
  align-self: flex-end;
  display: flex;
  margin-top: 30px;

  button {
    width: 150px;
    height: 35px;
    margin: 0 10px;
  }
}

</style>
