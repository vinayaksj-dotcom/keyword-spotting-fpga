# keyword-spotting-fpga
Based on the TensorFlow "Simple audio recognition" tutorial. 
Plan: modify the model, quantize it to INT8, and implement it in Verilog.
Dataset: Google Speech Commands (mini), download from
http://storage.googleapis.com/download.tensorflow.org/data/mini_speech_commands.zip
Float32: 84.0% | INT8 (post-training, 100 calibration samples): 76.8%
INT8 calibration 100 clips → 76.8%, 1280 clips → 67.2% (more calibration data hurt; investigating)
INT8 (post-training): 100 calibration clips → 76.8%, 320 → 68.4%, 1280 → 67.2%. Cause not yet understood.
20 epochs: float 83.7% (no gain over 10 epochs), INT8 67.5% (500 clips, random). Epoch count isn't the bottleneck.
