<template>
    <div @drop="dropped" @dragover.prevent @dragenter.prevent>
        <aside draggable="true" ref="dragme" @dragstart="dragStarted">
            This is an aside, drag me.
        </aside>
        <p>I never am really satisfied that I understand anything; because, understand it well as I may, my comprehension can only be an infinitesimal fraction of all I want to understand about the many connections and relations which occur to me, how the matter in question was first thought of or arrived at, etc., etc.</p>
        <p>In almost every computation a great variety of arrangements for the succession of the processes is possible, and various considerations must influence the selections amongst them for the purposes of a calculating engine. One essential object is to choose that arrangement which shall tend to reduce to a minimum the time necessary for completing the calculation.</p>
        <p>Many persons who are not conversant with mathematical studies imagine that because the business of [Babbage’s Analytical Engine] is to give its results in numerical notation, the nature of its processes must consequently be arithmetical and numerical, rather than algebraical and analytical. This is an error. The engine can arrange and combine its numerical quantities exactly as if they were letters or any other general symbols; and in fact it might bring out its results in algebraical notation, were provisions made accordingly.</p>
        <p>The Analytical Engine has no pretensions whatever to originate anything. It can do whatever we know how to order it to perform. It can follow analysis, but it has no power of anticipating any analytical revelations or truths. Its province is to assist us in making available what we are already acquainted with.</p>
        <button @click="testt()">Test</button>
    </div>
</template>

<script>
import { ref } from "vue"

export default {
    setup() {
        const dragme = ref(null)
        return {dragme}
    },
    data: () => ({}),
    methods: {
        dragStarted(event) {
        var style = window.getComputedStyle(event.target, null);
        event.dataTransfer.setData("text/plain",
        (parseInt(style.getPropertyValue("left"),10) - event.clientX) + ',' + (parseInt(style.getPropertyValue("top"),10) - event.clientY));
        console.log(style);
        },
        dropped(event) {
            var offset = event.dataTransfer.getData("text/plain").split(',');
            this.dragme.style.left = (event.clientX + parseInt(offset[0],10)) + 'px';
            this.dragme.style.top = (event.clientY + parseInt(offset[1],10)) + 'px';
            event.preventDefault();
            return false;
        },
    }
}
</script>

<style scoped>
aside { 
    position:  absolute;
    left: 0;
    top: 0; /* set these so Chrome doesn't return 'auto' from getComputedStyle */
    width: 200px; 
    background: rgba(255,255,255,0.66); 
    border: 2px  solid rgba(0,0,0,0.5); 
    border-radius: 4px; padding: 8px;
}
p {
    padding: 0;
    /* margin: 0; */
}
</style>
