# keyword-spotting-fpga
Based on the TensorFlow "Simple audio recognition" tutorial. 
Plan: modify the model, quantize it to INT8, and implement it in Verilog.
Dataset: Google Speech Commands (mini), download from
http://storage.googleapis.com/download.tensorflow.org/data/mini_speech_commands.zip
Float32: 84.0% | INT8 (post-training, 100 calibration samples): 76.8%
INT8 calibration 100 clips → 76.8%, 1280 clips → 67.2% (more calibration data hurt; investigating)
INT8 (post-training): 100 calibration clips → 76.8%, 320 → 68.4%, 1280 → 67.2%. Cause not yet understood.
20 epochs: float 83.7% (no gain over 10 epochs), INT8 67.5% (500 clips, random). Epoch count isn't the bottleneck.
QAT on Conv/Dense (4 epochs fine-tune): 83.2% vs post-training INT8 74-80%, float 84.0%. Model is 1.6M params, too large for on-chip BRAM; next: shrink the architecture.
## Results (test accuracy, 8 words)
- Float32 (10 epochs): 84.0%
- Float32 (20 epochs): 83.7% (no gain)
- Post-training INT8: 74-80% (depends on calibration clips)
- QAT on Conv/Dense layers (4 epochs fine-tune): 83.2%
## Notes
- Based on the TensorFlow "Simple audio recognition" tutorial.
- Model has 1.6M parameters, too large for on-chip BRAM. Next: shrink the architecture, then Verilog.
- QAT needs the first cell (tf_keras + TF_USE_LEGACY_KERAS) and "Restart session and run all".
- Dataset: http://storage.googleapis.com/download.tensorflow.org/data/mini_speech_commands.zip
