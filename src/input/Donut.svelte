<script lang="ts">
    import { Layer, type Render } from "svelte-canvas";
    import { input_store } from "../input/input_store";
    import { Vector, Matrix } from "ts-matrix";
    import * as s from "../settings/settings";

    let render: Render;
    function rotate3D(v: Vector, angle: number, axis: Vector): Vector {
        const c = Math.cos(angle);
        const s = Math.sin(angle);
        const t = 1 - c;
        const x = v.at(0);
        const y = v.at(1);
        const z = v.at(2);
        const u = axis.normalize();
        const a = new Matrix(3, 3, [
            [
                t * u.at(0) * u.at(0) + c,
                t * u.at(0) * u.at(1) - s * u.at(2),
                t * u.at(0) * u.at(2) + s * u.at(1),
            ],
            [
                t * u.at(0) * u.at(1) + s * u.at(2),
                t * u.at(1) * u.at(1) + c,
                t * u.at(1) * u.at(2) - s * u.at(0),
            ],
            [
                t * u.at(0) * u.at(2) - s * u.at(1),
                t * u.at(1) * u.at(2) + s * u.at(0),
                t * u.at(2) * u.at(2) + c,
            ],
        ]);
        const vMatrix = new Matrix(3, 1, [[x], [y], [z]]);
        const result = a.multiply(vMatrix);
        return new Vector([result.at(0, 0), result.at(1, 0), result.at(2, 0)]);
    }
    $: mouseVector = new Vector([
        Math.cos($input_store.angle),
        Math.sin($input_store.angle),
        0,
    ]);
    $: turnAngle = ($input_store.radius / s.radius) * Math.PI;

    $: render = ({ context, width, height }) => {
        const rootVector = new Vector([width / 2, height / 2, 0]);
        const slices = 64;
        const pointsPerSlice = 32;
        const bigRadius = 200;
        const smallRadius = 80;
        const stretch = 1.5;

        const lightVector = new Vector([1, 1, -1]).normalize();

        for (let i = 0; i < slices; i++) {
            const phi = (i / slices) * Math.PI * 2;
            const innerVector = new Vector([Math.cos(phi), Math.sin(phi), 0]);
            for (let j = 0; j < pointsPerSlice; j++) {
                const theta = (j / pointsPerSlice) * Math.PI * 2;
                const outerVector = innerVector
                    .scale(Math.sin(theta))
                    .add(new Vector([0, 0, Math.cos(theta) * stretch]));
                let sumVector = outerVector
                    .scale(smallRadius)
                    .add(innerVector.scale(bigRadius));
                sumVector = rotate3D(sumVector, turnAngle, mouseVector);
                const point = sumVector.add(rootVector);
                const shade = 0.8 + 0.2 * lightVector.dot(outerVector);
                const height = outerVector.at(2) / stretch;
                const fadeInfluence = 0.6;
                const fade = Math.min(
                    1,
                    1 -
                        fadeInfluence -
                        ((sumVector.at(2) / smallRadius) * fadeInfluence) / 2
                );
                context.fillStyle = `rgba(255, 100, ${255 * (0.75 + 0.5 * height)}, ${Math.min(shade * fade, 1)})`;
                context.fillRect(point.at(0), point.at(1), 5, 5);
            }
        }
    };
</script>

<Layer {render} />
