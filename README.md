# Stock Predictor

An exploratory time-series forecasting project that compares linear regression and LSTM neural networks for predicting stock closing prices. The notebooks analyze historical OHLCV data, visualize price trends and moving averages, train forecasting models, and export predictions for a 633-row forecast horizon.

> **Disclaimer:** This project is for educational and experimental purposes only. It is not financial advice, and its predictions should not be used as the sole basis for investment decisions.

## What the Project Does

The notebooks follow this general workflow:

1. Load historical stock CSV files from a Kaggle-style input directory.
2. Combine the files into four company datasets and assign company identifiers.
3. Explore closing prices, daily percentage changes, and moving averages.
4. Use `Open`, `High`, `Low`, `Adj Close`, and `Volume` as model features.
5. Scale input and target values to the `[0, 1]` range with `MinMaxScaler`.
6. Train linear regression baselines.
7. Build LSTM models using 60 historical time steps to predict closing prices.
8. Compare predicted and actual values with plots and a basic RMSE calculation.
9. Export predictions to CSV files for further analysis or competition submission.

## Repository Contents

```text
Stock-Predictor/
├── comp2-finalday.ipynb    # Stock analysis and forecasting experiments
├── comp3-finalday.ipynb    # Related experiment with revised notebook flow
├── comp4-finalday.ipynb    # Extended forecasting and export workflow
├── README.md               # Project documentation
└── LICENSE                 # Project license
```

The notebooks contain overlapping experiments for different company series. `comp4-finalday.ipynb` includes the most extensive workflow, including iterative LSTM forecasting and CSV export.

## Dataset Layout

The notebooks currently use the hard-coded path `/kaggle/input/stockp` and expect CSV files in that directory. The source files should contain columns similar to:

```text
Date, Open, High, Low, Close, Adj Close, Volume
```

The current code identifies company files using the first character of each filename. A file whose name begins with `t` is treated as a separate test/continuation dataset and is split across the four company series. If you run the project outside Kaggle, replace `/kaggle/input/stockp` in the notebooks with the local dataset path and verify the filename convention.

## Requirements

- Python 3.7 or later
- Jupyter Notebook or JupyterLab
- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- Keras with a TensorFlow backend

Install the main dependencies with:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn tensorflow jupyter
```

The notebooks use both `keras` and `tensorflow`-compatible APIs. If your environment does not provide the standalone `keras` package, update the imports to use `tensorflow.keras` consistently.

## Running the Notebooks

1. Download or prepare the historical stock CSV data.
2. Place the data in the expected directory, or update the path in each notebook.
3. Open one of the notebooks in Jupyter or VS Code.
4. Run the cells from top to bottom.
5. Review the visualizations, model outputs, and generated CSV files.

The notebooks are exploratory and contain cells that depend on variables created earlier. Running cells out of order may result in missing-variable errors.

## Models

### Linear Regression

The baseline uses the scaled OHLCV features to estimate the closing price for rows after the first 2,530 training records. The baseline is useful for comparison, but it does not model temporal dependencies explicitly.

### LSTM

The recurrent model uses:

- A 60-step historical window
- Five input features per time step
- One LSTM layer with 64 units
- One dense output unit for the predicted close
- Adam optimization
- Mean squared error loss

The notebooks train for four epochs in the included experiments. The iterative experiment retrains a new model for each forecast step, which can be computationally expensive and may produce different results between runs because random seeds are not fixed.

## Outputs

Depending on the notebook and cells executed, the project can generate files such as:

```text
jai633com3.csv
comp4_633.csv
```

These files contain an identifier column and predicted closing prices. Generated outputs are not included in the repository.

## Limitations

- Dataset paths and the filename-based company mapping are hard-coded.
- The notebooks do not provide a formal train/validation/test pipeline for every experiment.
- The reported RMSE calculation in the notebooks focuses on the first prediction in some LSTM sections rather than a full-horizon aggregate metric.
- The iterative forecasting code retrains repeatedly and is not optimized for speed.
- LSTM results can vary between runs because the random seeds and full reproducibility settings are not configured.
- Historical price patterns do not guarantee future performance.

## License

See [LICENSE](LICENSE) for the applicable license terms.
