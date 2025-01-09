# MVPBENCH

This repo contains code evaluation and dataset for the paper MVPBench: A Multi-Video Perception Evaluation Benchmark for Multi-modal Video Understanding

## Introduction
The rapid progress of Large Language Models (LLMs) has spurred growing interest in Multi-modal LLMs (MLLMs) and motivated the development of benchmarks to evaluate their perceptual and comprehension abilities. Existing benchmarks, however, are limited to static images or single videos, overlooking the complex interactions across multiple videos. To address this gap, we introduce the **M**ulti-**V**ideo **P**erception Evaluation **Bench**mark (**MVPBench**), a new benchmark featuring **14** subtasks across diverse visual domains that task models with extracting relevant information from video sequences to make informed decisions. MVPBench includes **1K** question-answering tests involving **2.7K** video clips sourced from existing datasets and manually annotated clips. Extensive evaluations reveal that current models struggle to process multi-video inputs effectively, underscoring substantial limitations in their multi-video comprehension. We anticipate MVPBench will drive advancements in multi-video perception.
![Dataset Overview](assets/Figure2.jpg)
## Dataset
MVPBench includes a diverse set of 14 subtasks that evaluate the model’s capabilities across various dimensions. These tasks range from basic to advanced levels, covering a variety of question-answering formats from low-level pattern recognition to high-level semantic interpretation, thereby imposing rigorous demands on model performance across perceptual and cognitive dimensions. During the design process, these tasks adhere to the design principles which emphasize the consideration of both the multiplicity of evaluation inputs and the temporal aspects of evaluation videos. This approach ensures that the tasks are structured to effectively assess models on their ability to manage diverse input types and to accurately interpret and utilize the timing and sequence of video data. 

All data is hosted on [google pan](https://drive.google.com/drive/folders/1geVRGz6SFT8726R0tpljdwf3kJxvFFza?usp=sharing) and is divided according to different task names and stored in zip compression format.

Statistics of MVPBench are shown below. The benchmark includes 14 tasks in 5 domains, ranging from low-level pattern comparison to mid-level temporal logic reasoning, and extending to high-level visual content understanding.
![Dataset Statistics](assets/Figure3.jpg)

## Evaluation
We adhere to the default inference settings of the [SWIFT](https://github.com/modelscope/ms-swift/tree/main) framework, utilizing the &lt;video&gt; placeholder to predefine the position of the input video within the prompt. This approach facilitates the integration of visual and language input, guiding the model accordingly. We employ a set of predefined rules along with GPT-3.5-turbo to extract the selected answer from the model’s output.

In the dataset files we provide, each file contains the original video files and the corresponding annotation file in jsonl format. The annotation file contains the following information (taking the Multiview visual perception pairing task as an example):
```
"id": "01209_f.mp4"
```
This means that this jsonl entry records the annotation information corresponding to the video file named '01209_f.mp4'. It is also the file name of the reference video in this task.
```
"query": "Please analyze the given reference video, Ref Video: <video> Compare it with the three candidate videos provided: Video 1: <video>Video 2: <video>Video 3: <video> The task is to identify the candidate video that corresponds to the reference video. The reference video is presented from a first-person perspective, while the correct candidate video is shown from a second-person perspective of the same scene. The other two candidate videos are considered distractors and do not match the reference video. Please examine each video closely and identify the candidate video that accurately matches the reference video. Provide your answer solely as a single digit that corresponds to the number of the correct candidate video, without any additional explanation or information."
```
This records the prompt that will be input into the SWIFT framework. The four &lt;video&gt placeholders indicate that the four video paths will be input in sequence during the framework's reasoning process.
```
"video_options": ["01209_s.mp4", "00460_s.mp4", "01043_s.mp4"]
```
This represents the file names of the three videos to be selected in the above query.
```
"options": ["1", "2", "3"]
```
This represents the input order of the three candidate videos. In this example, the three candidate videos will be input in sequence.
```
"answer": "1"
```
This corresponds to the "options" above, and records the serial number of the correct answer we expect the model to respond to the input prompt. This serial number is exactly one of the index relationships corresponding to "video_options" recorded in "options".

A complete enrty of the jsonl file is as follows:
```
{"id": "01209_f.mp4", "query": "Please analyze the given reference video, Ref Video: <video> Compare it with the three candidate videos provided: Video 1: <video>Video 2: <video>Video 3: <video> The task is to identify the candidate video that corresponds to the reference video. The reference video is presented from a first-person perspective, while the correct candidate video is shown from a second-person perspective of the same scene. The other two candidate videos are considered distractors and do not match the reference video. Please examine each video closely and identify the candidate video that accurately matches the reference video. Provide your answer solely as a single digit that corresponds to the number of the correct candidate video, without any additional explanation or information.", "video_options": ["01209_s.mp4", "00460_s.mp4", "01043_s.mp4"], "options": ["1", "2", "3"], "answer": "1"}
```

## Disclaimers
For some specific tasks in MVPBench, we manually collected images that are publicly available from online search. We have made every effort to ensure that the images included in this paper are used in accordance with applicable copyright laws and are properly credited. However, if you are the copyright owner of any image included in our work and believe that its use conflicts with your licensing agreements, please contact us directly. We are committed to addressing any legitimate concerns promptly.

