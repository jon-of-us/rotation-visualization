<script lang="ts">
    import { Layer, type Render } from "svelte-canvas";
    import { input_store } from "../input/input_store";
    import { Vector, Matrix } from "ts-matrix";
    import * as s from "../settings/settings";

    let render: Render;

    $: render = ({ context, width, height }) => {
        const rootVector = new Vector([width / 2, height / 2, 0]);
        const slices = 64;
        const pointsPerSlice = 32;
        const bigRadius = 200;
        const smallRadius = 80;

        const lightVector = new Vector([0, 0, 1]);

        for (let i = 0; i < slices; i++) {
            const phi = (i / slices) * Math.PI * 2;
            const innerVector = new Vector([
                (Math.cos(phi) * width) / 4,
                (Math.sin(phi) * height) / 4,
                0,
            ]);
            for (let j = 0; j < pointsPerSlice; j++) {
                const theta = (j / pointsPerSlice) * Math.PI * 2;
                const outerVector = innerVector
                    .scale(Math.sin(theta))
                    .add(new Vector([0, 0, Math.cos(theta)]));
                const point = rootVector
                    .add(outerVector.scale(bigRadius))
                    .add(innerVector.scale(smallRadius));
                const shade = 100 + 155 * lightVector.dot(outerVector);
                context.fillStyle = `rgb(${shade}, ${shade}, ${shade})`;
                context.beginPath();
                context.arc(point.at(0), point.at(1), 2, 0, Math.PI * 2);
            }
        }
    };
</script>

<Layer {render} />
