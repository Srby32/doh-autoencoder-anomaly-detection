# doh-autoencoder-anomaly-detection
Anomaly Detection in DNS over HTTPS Traffic Using an Autoencoder-Based Approach
# DoH Anomaly Detection with an Autoencoder

This repository contains code for detecting malicious DNS over HTTPS (DoH) traffic
with an autoencoder. The autoencoder is trained only on benign DoH traffic.
A flow is flagged as malicious when its reconstruction error is above a threshold.
All features can be computed in real time while packets arrive.

## Contents

| Folder | Description |
|---|---|
| `feature_selection` | Selects features by removing one feature at a time and checking the AUC on a tuning set. No labels are used during training. |
| `zeek_feature_extraction` | Zeek script that computes the 16 flow features from live traffic. Flows are split with a 40 second idle timeout and a 90 second duration limit. |
| `live_monitor` | Reads the features produced by Zeek and scores each flow with the trained model. Flows with fewer than five packets are not scored. |
| `diagnostics` | Shows how much each feature contributes to the reconstruction error of a flow. |

## Dataset

The code uses the BCCC-CIRA-CIC-DoHBrw-2020 dataset [1],
which is a balanced version of the CIRA-CIC-DoHBrw-2020 dataset [2].
After downloading the dataset, set `DATA_PATH` at the top of each script.

[1] S. Niktabe, A. H. Lashkari, and A. H. Roudsari, "Unveiling DoH tunnel: Toward generating a balanced DoH encrypted traffic dataset and profiling malicious behavior using inherently interpretable machine learning," *Peer-to-Peer Networking and Applications*, vol. 17, no. 1, pp. 507–531, 2024.

[2] M. MontazeriShatoori, L. Davidson, G. Kaur, and A. H. Lashkari, "Detection of DoH tunnels using time-series classification of encrypted traffic," in *2020 IEEE Intl Conf on Dependable, Autonomic and Secure Computing (DASC/PiCom/CBDCom/CyberSciTech)*, pp. 63–70, 2020.

## Requirements

- Python 3.10
- Zeek (for live feature extraction)

## Reproducibility

All data splits use `random_state=42`.


## License

MIT License. See `LICENSE`.
