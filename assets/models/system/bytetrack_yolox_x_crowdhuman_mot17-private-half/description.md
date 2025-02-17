`bytetrack_yolox_x_crowdhuman_mot17-private-half` model is from <a href="https://github.com/open-mmlab/mmtracking/tree/v0.14.0" target="_blank">OpenMMLab's MMTracking library</a>. This model is <a href="https://github.com/open-mmlab/mmtracking/blob/master/configs/mot/bytetrack/metafile.yml#L24" target="_blank">reported</a> to obtain MOTA: 78.6, IDF1: 79.2 for video-multi-object-tracking task on <a href="https://motchallenge.net/data/MOT17/" target="_blank">MOT17-half-eval dataset</a>.

Multi-object tracking (MOT) aims at estimating bounding boxes and identities of objects in videos. Most methods obtain identities by associating detection boxes whose scores are higher than a threshold. The objects with low detection scores, e.g. occluded objects, are simply thrown away, which brings non-negligible true object missing and fragmented trajectories. To solve this problem, we present a simple, effective and generic association method, tracking by associating every detection box instead of only the high score ones. For the low score detection boxes, we utilize their similarities with tracklets to recover true objects and filter out the background detections. When applied to 9 different state-of-the-art trackers, our method achieves consistent improvement on IDF1 score ranging from 1 to 10 points. To put forwards the state-of-the-art performance of MOT, we design a simple and strong tracker, named ByteTrack. For the first time, we achieve 80.3 MOTA, 77.3 IDF1 and 63.1 HOTA on the test set of MOT17 with 30 FPS running speed on a single V100 GPU.

> The above abstract is from MMTracking website. Review the <a href="https://github.com/open-mmlab/mmtracking/tree/v0.14.0/configs/mot/bytetrack" target="_blank">original-model-card</a> to understand the data used to train the model, evaluation metrics, license, intended uses, limitations and bias before using the model.

### Inference samples

Inference type|Python sample (Notebook)|CLI with YAML
|--|--|--|
Real time|<a href="https://aka.ms/azureml-video-mutli-object-tracking-online-inference" target="_blank">video-multi-object-tracking-online-endpoint.ipynb</a>|<a href="https://aka.ms/cli-video-multi-object-tracking-online-inference" target="_blank">video-multi-object-tracking-online-endpoint.sh</a>|

### Finetuning samples

Task|Use case|Dataset|Python sample (Notebook)|CLI with YAML
|---|--|--|--|--|
Video multi-object tracking|Video multi-object tracking|[MOT17 tiny](https://download.openmmlab.com/mmtracking/data/MOT17_tiny.zip)|<a href="https://aka.ms/azureml-video-multi-object-tracking-finetune" target="_blank">mot17-tiny-video-multi-object-tracking.ipynb</a>|<a href="https://aka.ms/cli-video-multi-object-tracking-finetune" target="_blank">mot17-tiny-video-multi-object-tracking.sh</a>|


### Sample inputs and outputs (for real-time inference)

#### Sample input

```json
{
  "input_data": {
    "columns": [
      "video"
    ],
    "data": ["video_link"]
  }
}
```

Note: "video_link" should be a publicly accessible url.

#### Sample output

```json
[
  {
    "det_bboxes": [
      {
        "box": {
          "topX": 703.9149780273,
          "topY": -5.5951070786,
          "bottomX": 756.9875488281,
          "bottomY": 158.1963806152
        },
        "label": 0,
        "score": 0.9597821236
      },
      {
        "box": {
          "topX": 1487.9072265625,
          "topY": 67.9468841553,
          "bottomX": 1541.1591796875,
          "bottomY": 217.5476837158
        },
        "label": 0,
        "score": 0.9568068385
      }
    ],
    "track_bboxes": [
      {
        "box": {
          "instance_id": 0,
          "topX": 703.9149780273,
          "topY": -5.5951070786,
          "bottomX": 756.9875488281,
          "bottomY": 158.1963806152
        },
        "label": 0,
        "score": 0.9597821236
      },
      {
        "box": {
          "instance_id": 1,
          "topX": 1487.9072265625,
          "topY": 67.9468841553,
          "bottomX": 1541.1591796875,
          "bottomY": 217.5476837158
        },
        "label": 0,
        "score": 0.9568068385
      }
    ],
    "frame_id": 0,
    "video_url": "video_link"
  }
]
```

#### Model inference - visualization for a video

<img src="https://automlcesdkdataresources.blob.core.windows.net/finetuning-image-models/images/Model_Result_Visualizations(Do_not_delete)/plot_mot_b2d502aa-f0b28e3e.gif" alt="mot visualization">