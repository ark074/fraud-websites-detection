# Fraud Websites Detection System

A machine learning-based web application designed to detect phishing and fraudulent websites using advanced URL feature extraction and classification algorithms.

## Overview

This project implements a sophisticated phishing URL detection system that analyzes URLs using 30 distinct features derived from URL structure, domain characteristics, and page content indicators. The system employs a Gradient Boosting Classifier model to classify websites as legitimate (safe) or fraudulent (phishing) with probabilistic confidence scores.

## Features

### URL Analysis Features (30 Feature Set)

The system extracts and analyzes the following feature categories:

#### URL-Based Features
1. **Using IP Address** - Detects if URL uses IP address instead of domain
2. **URL Length** - Analyzes URL length for phishing patterns
3. **Short URL Service** - Identifies use of URL shortening services
4. **@ Symbol Usage** - Detects presence of @ symbol in URL
5. **Redirecting (//)** - Checks for multiple redirects in URL structure
6. **Prefix-Suffix Hyphen** - Detects hyphen characters in domain
7. **Sub-Domains** - Analyzes subdomain count and structure

#### HTTPS and Security Features
8. **HTTPS Protocol** - Validates HTTPS implementation
9. **HTTPS in Domain** - Checks for HTTPS indicators in domain name
10. **Domain Registration Length** - Analyzes domain registration period

#### Domain and Server Features
11. **Non-Standard Port** - Detects usage of non-standard ports
12. **Favicon** - Analyzes favicon source and consistency
13. **Domain Registration Info** - Examines WHOIS registration details
14. **DNS Recording** - Validates DNS record age

#### Content-Based Features
15. **Request URL** - Analyzes image, audio, embed, and iframe sources
16. **Anchor URL** - Examines hyperlink destinations
17. **Links in Script Tags** - Analyzes links in script and link tags
18. **Server Form Handler** - Examines form submission handlers
19. **Info Email** - Detects email addresses in content

#### Web Behavior Features
20. **Abnormal URL** - Compares URL and content patterns
21. **Website Forwarding** - Analyzes page redirect chains
22. **Status Bar Customization** - Detects JavaScript status bar manipulation
23. **Right Click Disable** - Detects disabled right-click functionality
24. **Popup Windows** - Detects popup window usage
25. **IFrame Redirection** - Analyzes iframe and frame usage

#### Reputation Features
26. **Website Traffic** - Checks Alexa ranking and traffic
27. **Page Rank** - Analyzes Google PageRank
28. **Google Index** - Validates presence in Google search index
29. **Links Pointing to Page** - Counts inbound links
30. **Statistics Report** - Cross-references against phishing databases

## System Architecture

### Components

- **`feature.py`** - Feature extraction module implementing 30-feature URL analysis
- **`app.py`** - Flask web application server
- **`model.pkl`** - Pre-trained Gradient Boosting Classifier model
- **`phishing.csv`** - Training dataset containing URL samples and labels
- **`Phishing URL Detection.ipynb`** - Jupyter notebook with model development and analysis

### Technology Stack

- **Web Framework**: Flask
- **Machine Learning**: scikit-learn (Gradient Boosting)
- **Data Processing**: NumPy, Pandas
- **Web Parsing**: BeautifulSoup4
- **Network Analysis**: WHOIS, DNS, socket libraries
- **Search Integration**: Google Search API
- **Deployment**: Gunicorn, Heroku (via Procfile)

## Installation

### Prerequisites
- Python 3.7 or higher
- pip package manager

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/ark074/fraud-websites-detection.git
   cd fraud-websites-detection
   ```

2. **Create virtual environment** (recommended)
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Running the Application

#### Local Development
```bash
python app.py
```
The application will start on `http://localhost:5000`

#### Production Deployment
```bash
gunicorn app:app
```

### Web Interface

1. Navigate to the application URL
2. Enter a URL in the input form
3. Submit for analysis
4. View the phishing probability score and safety assessment

### Feature Output

The system returns:
- **Phishing Probability**: Confidence percentage that the URL is safe
- **Safety Assessment**: Binary classification (Safe/Unsafe)
- **Detailed Analysis**: Feature-level breakdown of URL characteristics

## Model Training

The pre-trained model (`model.pkl`) was trained using:
- **Algorithm**: Gradient Boosting Classifier
- **Features**: 30 URL-based indicators
- **Dataset**: Phishing URL dataset (`phishing.csv`)
- **Performance**: Validated accuracy on test dataset

To retrain the model, refer to the Jupyter notebook: `Phishing URL Detection.ipynb`

## Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| Flask | ≥2.0.0 | Web framework |
| Gunicorn | 22.0.0 | WSGI server |
| scikit-learn | 1.5.2 | Machine learning |
| NumPy | 2.1.2 | Numerical computing |
| Pandas | 2.2.3 | Data manipulation |
| BeautifulSoup4 | 4.9.3 | HTML parsing |
| requests | 2.25.1 | HTTP requests |
| whois | 2024.01.29 | WHOIS queries |
| python-dateutil | 2.8.2 | Date utilities |
| googlesearch-python | 1.0.1 | Google search API |

## Project Structure

```
fraud-websites-detection/
├── app.py                          # Flask application
├── feature.py                      # Feature extraction module
├── model.pkl                       # Pre-trained classifier model
├── phishing.csv                    # Training dataset
├── Phishing URL Detection.ipynb    # Model development notebook
├── requirements.txt                # Python dependencies
├── Procfile                        # Heroku deployment config
├── runtime.txt                     # Python runtime version
├── templates/                      # HTML templates
│   └── index.html                 # Web interface
└── static/                        # Static assets
    ├── CSS/                       # Stylesheets
    └── JS/                        # JavaScript files
```

## API Response Format

### Input
- **Parameter**: `url` (string)
- **Method**: POST

### Output
```json
{
  "url": "https://example.com",
  "phishing_probability": 0.95,
  "classification": "Safe",
  "confidence": 95
}
```

## Limitations and Considerations

1. **Feature Dependency**: Accuracy depends on access to external APIs (WHOIS, Google Search, Alexa)
2. **Dynamic Content**: Limited ability to analyze JavaScript-rendered content
3. **URL Obfuscation**: May struggle with highly obfuscated URLs
4. **False Positives**: New or legitimate but unusual websites may be misclassified
5. **API Rate Limiting**: External API calls may be rate-limited

## Performance Metrics

The model achieves:
- High recall for phishing detection
- Low false negative rate
- Balanced precision for production use

Refer to the Jupyter notebook for detailed performance analysis and confusion matrices.

## Future Enhancements

- Integration with real-time threat intelligence feeds
- Support for dynamic content analysis using Selenium
- Enhanced feature engineering for zero-day phishing detection
- Machine learning model optimization and ensemble methods
- API endpoint for programmatic access
- Browser extension for real-time URL checking

## Security Disclaimer

This tool is designed for educational and security research purposes. While it provides probabilistic assessments, it should not be relied upon as the sole security mechanism. Always exercise caution when visiting unfamiliar websites and maintain comprehensive security practices.

## Contributing

Contributions are welcome. Please ensure:
1. Code follows PEP 8 style guidelines
2. All new features include appropriate error handling
3. Documentation is updated accordingly
4. Testing is performed before submission

## License

This project is open source and available under standard open source licensing. Refer to LICENSE file for details.

## Author

**ark074**  
GitHub: [@ark074](https://github.com/ark074)

## Acknowledgments

- Dataset sourced from phishing URL repositories
- Feature engineering based on academic research in phishing detection
- Community contributions and feedback

## Support and Issues

For issues, feature requests, or questions:
1. Check existing GitHub issues
2. Create a detailed new issue with:
   - Clear problem description
   - Steps to reproduce
   - Expected vs. actual behavior
   - System information

## References

- Phishing Detection Research Papers
- scikit-learn Machine Learning Documentation
- OWASP Web Security Guidelines
- URL Analysis and Feature Engineering Studies

---

**Last Updated**: 2026-04-29  
**Repository**: https://github.com/ark074/fraud-websites-detection
