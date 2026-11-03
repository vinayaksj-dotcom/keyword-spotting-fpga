# keyword-spotting-fpga
Based on the TensorFlow "Simple audio recognition" tutorial. 
Plan: modify the model, quantize it to INT8, and implement it in Verilog.
Dataset: Google Speech Commands (mini), download from
http://storage.googleapis.com/download.tensorflow.org/data/mini_speech_commands.zip
Float32: 84.0% | INT8 (post-training, 100 calibration samples): 76.8%
Float32: 84.0%
INT8, ~100 clips: 76.8%
INT8, ~1,280 clips: 67.2%
