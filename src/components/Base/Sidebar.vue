<template>
  <div class="hidden">
    <!--
    SideBar
    -->
    <vs-sidebar absolute open reduce background="#011826" textWhite>
      <vs-sidebar-group>
        <template #header>
          <vs-sidebar-item arrow>
            <template #icon>
              <MicrosoftWindowsClassic />
            </template>
            Sistema
          </vs-sidebar-item>
        </template>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <RocketLaunchOutline @click="abrirDialog('abrirPrograma')" />
          </template>
          <p @click="abrirDialog('abrirPrograma')">Abrir programa</p>
        </vs-sidebar-item>
      </vs-sidebar-group>

      <vs-sidebar-group>
        <template #header>
          <vs-sidebar-item arrow>
            <template #icon>
              <VolumeHigh />
            </template>
            Audio
          </vs-sidebar-item>
        </template>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <PlayBoxMultipleOutline @click="abrirDialog('reproducirAudio')" />
          </template>
          <p @click="abrirDialog('reproducirAudio')">Reproducir audio</p>
        </vs-sidebar-item>
      </vs-sidebar-group>

      <vs-sidebar-group>
        <template #header>
          <vs-sidebar-item arrow>
            <template #icon>
              <Discord />
            </template>
            Discord
          </vs-sidebar-item>
        </template>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <MicrophoneOff @click="abrirDialog('muteDiscord')" />
          </template>
          <p @click="abrirDialog('muteDiscord')">Microfono Discord (Toggle)</p>
        </vs-sidebar-item>
      </vs-sidebar-group>

      <vs-sidebar-group>
        <template #header>
          <vs-sidebar-item arrow>
            <template #icon>
              <Spotify />
            </template>
            Multimedia
          </vs-sidebar-item>
        </template>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <PlayPause @click="abrirDialog('playPause')" />
          </template>
          <p @click="abrirDialog('playPause')">Opciones multimedia</p>
        </vs-sidebar-item>
      </vs-sidebar-group>

      <vs-sidebar-group>
        <template #header>
          <vs-sidebar-item arrow>
            <template #icon>
              <LightbulbMultipleOutline />
            </template>
            Govee
          </vs-sidebar-item>
        </template>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <LightbulbOnOutline @click="abrirDialog('apagarLuces')" />
          </template>
          <p @click="abrirDialog('apagarLuces')">Apagar luces</p>
        </vs-sidebar-item>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <LightbulbOn @click="abrirDialog('prenderLuces')" />
          </template>
          <p @click="abrirDialog('prenderLuces')">Prender luces</p>
        </vs-sidebar-item>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <Palette @click="abrirDialog('cambiarColor')" />
          </template>
          <p @click="abrirDialog('cambiarColor')">Cambiar color</p>
        </vs-sidebar-item>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <Brightness5 @click="abrirDialog('cambiarBrillo')" />
          </template>
          <p @click="abrirDialog('cambiarBrillo')">Cambiar brillo</p>
        </vs-sidebar-item>
      </vs-sidebar-group>

      <vs-sidebar-group>
        <template #header>
          <vs-sidebar-item arrow>
            <template #icon>
              <RecordRec />
            </template>
            OBS Studio
          </vs-sidebar-item>
        </template>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <MicrophoneOff @click="abrirDialog('muteOBS')" />
          </template>
          <p @click="abrirDialog('muteOBS')">Microfono OBS (Toggle)</p>
        </vs-sidebar-item>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <Twitch @click="abrirDialog('startStream')" />
          </template>
          <p @click="abrirDialog('startStream')">Empezar stream</p>
        </vs-sidebar-item>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <Twitch @click="abrirDialog('stopStream')" />
          </template>
          <p @click="abrirDialog('stopStream')">Finalizar stream</p>
        </vs-sidebar-item>

        <vs-sidebar-item id="Abrir">
          <template #icon>
            <MovieOpenOutline @click="abrirDialog('changeScene')" />
          </template>
          <p @click="abrirDialog('changeScene')">Cambiar escena</p>
        </vs-sidebar-item>
      </vs-sidebar-group>

      <template #footer>
        <vs-row justify="space-between"> </vs-row>
      </template>
    </vs-sidebar>

    <AbrirPrograma v-if="iniciador == 'abrirPrograma'" :active="active" />
    <ReproducirAudio v-if="iniciador == 'reproducirAudio'" :active="active" />
    <MuteDiscord v-if="iniciador == 'muteDiscord'" :active="active" />
    <PlayPauseDialog v-if="iniciador == 'playPause'" :active="active" />
    <PrenderLuces v-if="iniciador == 'prenderLuces'" :active="active" />
    <ApagarLuces v-if="iniciador == 'apagarLuces'" :active="active" />
    <CambiarColor v-if="iniciador == 'cambiarColor'" :active="active"/>
    <CambiarBrillo v-if="iniciador == 'cambiarBrillo'" :active="active" />
    <MuteOBS v-if="iniciador == 'muteOBS'" :active="active" />
    <StartStream v-if="iniciador == 'startStream'" :active="active" />
    <ChangeScene v-if="iniciador == 'changeScene'" :active="active" />
    <StopStream v-if="iniciador == 'stopStream'" :active="active" />

  </div>
</template>

<script>
import MicrosoftWindowsClassic from "vue-material-design-icons/MicrosoftWindowsClassic.vue";
import RocketLaunchOutline from "vue-material-design-icons/RocketLaunchOutline.vue";
import VolumeHigh from "vue-material-design-icons/VolumeHigh.vue";
import PlayBoxMultipleOutline from "vue-material-design-icons/PlayBoxMultipleOutline.vue";
import MicrophoneOff from "vue-material-design-icons/MicrophoneOff.vue";
import Discord from "vue-material-design-icons/Discord.vue";
import Spotify from "vue-material-design-icons/Spotify.vue";
import PlayPause from "vue-material-design-icons/PlayPause.vue";
import LightbulbOnOutline from "vue-material-design-icons/LightbulbOnOutline.vue";
import LightbulbMultipleOutline from "vue-material-design-icons/LightbulbMultipleOutline.vue";
import LightbulbOn from "vue-material-design-icons/LightbulbOn.vue";
import Palette from "vue-material-design-icons/Palette.vue";
import Brightness5 from "vue-material-design-icons/Brightness5.vue";
import RecordRec from "vue-material-design-icons/RecordRec.vue"
import Twitch from "vue-material-design-icons/Twitch.vue"
import MovieOpenOutline from "vue-material-design-icons/MovieOpenOutline.vue"

import AbrirPrograma from "../Dialogs/AbrirPrograma.vue";
import ReproducirAudio from "../Dialogs/ReproducirAudio.vue";
import MuteDiscord from "../Dialogs/MuteDiscord.vue";
import PlayPauseDialog from "../Dialogs/PlayPauseDialog.vue";
import PrenderLuces from "../Dialogs/PrenderLuces.vue"
import ApagarLuces from "../Dialogs/ApagarLuces.vue"
import CambiarColor from "../Dialogs/CambiarColor.vue"
import CambiarBrillo from "../Dialogs/CambiarBrillo.vue"
import MuteOBS from "../Dialogs/MuteObs.vue"
import StartStream from "../Dialogs/IniciarStream.vue"
import ChangeScene from "../Dialogs/CambiarEscena.vue"
import StopStream from "../Dialogs/StopStream.vue"

export default {
  components: {
    MicrosoftWindowsClassic,
    RocketLaunchOutline,
    VolumeHigh,
    PlayBoxMultipleOutline,
    Discord,
    MicrophoneOff,
    Spotify,
    PlayPause,
    LightbulbOnOutline,
    LightbulbMultipleOutline,
    LightbulbOn,
    Palette,
    Brightness5,
    RecordRec,
    Twitch,
    MovieOpenOutline,
    MuteOBS,
    PlayPauseDialog,
    AbrirPrograma,
    ReproducirAudio,
    MuteDiscord,
    PrenderLuces,
    ApagarLuces,
    CambiarColor,
    CambiarBrillo,
    StartStream,
    ChangeScene,
    StopStream
  },
  data: () => ({
    active: false,
    iniciador: "",
  }),
  methods: {
    abrirDialog(iniciador) {
      this.active = true
      this.iniciador = iniciador;      
    },
    close(){
      this.active = false
    }
  },
}; 
</script>

<style scoped>
.dialog {
  background-color: #181818 !important;
}

.inputDialog {
  margin-top: 15px;
  width: 100% !important;
}

.buttonDialog {
  margin-top: 15px;
}

.vs-input {
  width: 100% !important;
}
</style>
