# Discovery research context

Checked: 2026-11-05. **Context only; these are not approved Lost and Found requirements.** This is a narrow capability scan, not market validation or a recommendation.

## Manual camera robot teleoperation

Hello Robot publishes a Stretch 4 browser teleoperation interface. Its official repository documents operation over a local network or internet, compatibility with Stretch 4 on Ubuntu 24.04/ROS2 Jazzy, and a single connected operator browser. It also describes robot video streams in its developer documentation and labels remote-use code a prototype. This establishes an available implementation example of remote operation with visual feedback; it does not establish compatibility with an Arduino/HC-05 robot or readiness for this product. Source: [Hello Robot Stretch 4 Web Teleop](https://github.com/hello-robot/stretch4_web_teleop).

## Reference-image object recognition

The YOLOE authors publish a visual-prompt prediction example that defines bounding boxes in a source image, obtains visual prompt embeddings, and applies them to a different target image. This is published example code, not evidence of reliable identification of a particular person's belonging. Source: [YOLOE visual-prompt prediction example](https://github.com/THU-MIG/yoloe/blob/main/predict_visual_prompt.py).

The authors' demonstration interface includes cross-image visual prompting and selection through bounding boxes or masks, followed by detection output. This is a relevant interaction precedent for a selected target within an uploaded image; it supplies no product-specific accuracy, laptop throughput, or camera-condition guarantee. Source: [YOLOE demonstration application](https://github.com/THU-MIG/yoloe/blob/main/app.py).

## Implications to clarify in the interview

Potential fit remains unverified. Clarify whether success means finding a similar object category or the exact belonging, how the user verifies a candidate, and the operating conditions used to judge results. Obtain explicit user decisions on video freshness, command loss, and motion stopping. No transport, model, platform, performance target, or feature is adopted from this scan.
