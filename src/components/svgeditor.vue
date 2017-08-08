<template>
    <div>
        <svg id="svg" viewBox="0 0 100 60" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
            <image xlink:href="../assets/markZ-01.png"
                height="60" width="100" />
            <g>
                <text x="55" y="34" font-color="black" font-size="3" text-anchor="middle">
                    <tspan x="55" dy="1.2em" >{{fathername}}</tspan>
                    <tspan x="55" dy="1.2em" >{{fathername}}</tspan>
                    <tspan x="55" dy="1.2em" >{{fathername}}</tspan>
                </text>
            </g>
        </svg>
    </div>
</template>
<script>
import { bus } from "../bus"

function chunkSubstr(str, size) {
    var numChunks = Math.ceil(str.length / size),
        chunks = new Array(numChunks);

    for (var i = 0, o = 0; i < numChunks; ++i, o += size) {
        chunks[i] = str.substr(o, size);
    }

    return chunks;
}
export default {
    props: {
        fathername: ''

    },
    mounted() {
        bus.$on('download', (id) => {
            this.download()
        })
    },
    methods: {
        download: function () {
            var can = document.createElement("canvas")
            var img = document.getElementsByTagName('img')[0];  // http://web.mit.edu/remy/
            var text = document.getElementsByTagName("tspan")
            for (var i = 0; i < text.length; i++) {
                text[i].textContent = unescape(encodeURIComponent(text[i].textContent))
            }
            var svg = document.getElementsByTagName("svg")[0];
            var svg_xml = (new XMLSerializer).serializeToString(svg);   // extract the data as SVG text
            var data_uri = "data:image/svg+xml;base64," + window.btoa(svg_xml);

            var image = new Image;
            image.src = data_uri;
            image.onload = function () {
                var canvas = document.createElement("canvas");
                canvas.width = 640;
                canvas.height = 480;

                var context = canvas.getContext("2d");
                context.clearRect(0, 0, 640, 480);
                context.drawImage(image, 0, 0);

                var a = document.createElement("a");
                a.download = "file.png";
                a.href = canvas.toDataURL("image/png");
                a.click();
                 bus.$emit('reset', 1)
            }.bind(this);

        }
    }
}
</script>

