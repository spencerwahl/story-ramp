<template>
    <div :class="ratio && config.type !== 'text' ? 'flex-2' : 'flex'" class="flex-col">
        <component :is="getTemplate()" :config="config" :slideIdx="slideIdx"></component>
    </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';

import { PanelType, BasePanel } from '@/definitions';
import TextPanelV from './text-panel.vue';
import MapPanelV from './map-panel.vue';
import ImagePanelV from './image-panel.vue';
import AudioPanelV from './audio-panel.vue';
import VideoPanelV from './video-panel.vue';
import SlideshowPanelV from './slideshow-panel.vue';
import ChartPanelV from './chart-panel.vue';
import DynamicPanelV from './dynamic-panel.vue';

@Component({
    components: {
        TextPanelV
    }
})
export default class PanelV extends Vue {
    @Prop() config!: BasePanel;
    @Prop() ratio!: boolean;
    @Prop() slideIdx!: number;

    /**
     * Returns the corresponding component for this panel.
     */
    getTemplate(): string {
        const panelTemplates: any = {
            [PanelType.Text]: TextPanelV,
            [PanelType.Map]: MapPanelV,
            [PanelType.Image]: ImagePanelV,
            [PanelType.Audio]: AudioPanelV,
            [PanelType.Video]: VideoPanelV,
            [PanelType.Slideshow]: SlideshowPanelV,
            [PanelType.Chart]: ChartPanelV,
            [PanelType.Dynamic]: DynamicPanelV
        };

        return panelTemplates[this.config.type];
    }
}
</script>

<style lang="scss" scoped></style>
