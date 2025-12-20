# Quick Start Guide

Get up and running with the Governance-by-Design framework in 5 minutes.

## 🚀 Installation

### 1. Clone Repository

```bash
git clone https://github.com/yourusername/governance-security-by-design.git
cd governance-security-by-design
```

### 2. Create Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Package

```bash
pip install -e .
```

### 4. Configure Environment

```bash
cp .env.example .env
# Edit .env and add your API keys
```

## 🎯 Basic Usage

### Example 1: Secure Code Generation

```python
from governance_framework import GovernanceEngine, GovernanceMode
from governance_framework.agents import SecurityAuditor
from governance_framework.agents.task import CodeGenerationAgent

# Initialize governance engine
engine = GovernanceEngine(mode=GovernanceMode.ADAPTIVE_INTEGRATION)

# Add security auditor
engine.register_agent(SecurityAuditor(
    vulnerability_patterns=["memory_safety", "crypto_errors"]
))

# Create code generation agent
agent = CodeGenerationAgent(model="gpt-4", temperature=0.2)

# Generate code with governance
result = engine.execute(
    agent=agent,
    task="Implement secure user authentication with password hashing",
    prompting_strategy="balanced"
)

# View results
print(f"Security Score: {result.security_score:.2f}")
print(f"Vulnerabilities Found: {len(result.vulnerabilities)}")
print(f"Code:\n{result.output}")
```

### Example 2: Preventing Iterative Degradation

```python
from governance_framework.agents import IterationGuardian

# Add iteration guardian
engine.register_agent(IterationGuardian(
    max_iterations=5,
    degradation_threshold=0.15
))

# Iteratively refine code
for iteration in range(10):
    result = engine.execute(
        agent=agent,
        task=f"Improve the authentication code (iteration {iteration})",
        prompting_strategy="balanced"
    )
    
    # Guardian will intervene if degradation detected
    if result.interventions:
        print(f"Intervention at iteration {iteration}")
        break
```

### Example 3: Managing Context Dilution

```python
from governance_framework.agents import ContextManager

# Add context manager
engine.register_agent(ContextManager(
    dilution_threshold=8000,
    decay_coefficient=0.0147
))

# Long conversation with maintained security focus
conversation_history = []
for turn in range(20):
    result = engine.execute(
        agent=agent,
        task=get_next_task(turn),
        prompting_strategy="balanced"
    )
    conversation_history.append(result)
```

## 📊 Running Experiments

### Vulnerability Pattern Analysis

```bash
python experiments/vulnerability_patterns.py \
    --samples 10 \
    --strategies efficiency,security,balanced \
    --output results/test.json
```

### With Governance Comparison

```bash
# Without governance
python experiments/vulnerability_patterns.py \
    --samples 10 \
    --output results/ungoverned.json

# With governance
python experiments/vulnerability_patterns.py \
    --samples 10 \
    --output results/governed.json \
    --with-governance
```

### View Results

```bash
python -c "
import json
with open('results/governed.json') as f:
    data = json.load(f)
    print(json.dumps(data['summary'], indent=2))
"
```

## 🔍 Analyzing Results

### Convergence Analysis

```python
# Get convergence metrics
metrics = engine.get_convergence_metrics()

print(f"Eigenvalues: {metrics['eigenvalues']}")
print(f"Convergence Rate: {metrics['convergence_rate']}")
print(f"Is Stable: {metrics['is_stable']}")
```

### Interference Matrix

```python
# Get multi-objective coupling
I = engine.get_interference_matrix()

print("Interference Matrix:")
print(I)

# Analyze coupling
from governance_framework.interference_matrix import InterferenceMatrix
analyzer = InterferenceMatrix()
coupling = analyzer.analyze_coupling(I)

print(f"Security-Functionality coupling: {coupling['security_functionality']}")
```

## 🎨 Visualizations

### Plot Trajectory

```python
import matplotlib.pyplot as plt
import numpy as np

# Extract trajectory
trajectory = np.array([
    [s.security, s.efficiency, s.functionality]
    for s in result.trajectory
])

# Plot
plt.figure(figsize=(10, 6))
plt.plot(trajectory[:, 0], label='Security')
plt.plot(trajectory[:, 1], label='Efficiency')
plt.plot(trajectory[:, 2], label='Functionality')
plt.xlabel('Iteration')
plt.ylabel('Objective Value')
plt.legend()
plt.title('Multi-Objective Dynamics')
plt.savefig('trajectory.png')
```

### Compare Strategies

```python
from governance_framework.utils.visualization import plot_strategy_comparison

plot_strategy_comparison(
    results=[result_efficiency, result_security, result_balanced],
    strategies=['Efficiency', 'Security', 'Balanced'],
    save_path='comparison.png'
)
```

## 🧪 Testing

### Run Tests

```bash
# All tests
pytest

# Specific test
pytest tests/test_engine.py::TestGovernanceEngine::test_initialization

# With coverage
pytest --cov=governance_framework --cov-report=html
```

### Verify Installation

```bash
python -c "
from governance_framework import GovernanceEngine
print('✓ Installation successful')
print(f'Version: {GovernanceEngine.__module__}')
"
```

## 📚 Next Steps

1. **Read the [Full Documentation](docs/API.md)** for detailed API reference

2. **Explore [Examples](examples/)** for more use cases:
   - Healthcare diagnostics
   - Financial risk assessment
   - Multi-modal AI systems

3. **Run [Full Experiments](scripts/run_all_experiments.sh)** to reproduce paper results

4. **Check [Contributing Guide](docs/CONTRIBUTING.md)** to contribute

## ⚠️ Common Issues

### API Key Not Found

```bash
# Error: OpenAI API key not set
export OPENAI_API_KEY=your_key_here

# Or add to .env file
echo "OPENAI_API_KEY=your_key_here" >> .env
```

### Import Errors

```bash
# Reinstall in development mode
pip install -e .

# Or install with all dependencies
pip install -e ".[dev]"
```

### Module Not Found

```bash
# Verify installation
pip list | grep governance

# Check Python path
python -c "import sys; print('\n'.join(sys.path))"
```

## 💡 Tips

1. **Start Simple**: Begin with a single governance agent, then add more

2. **Monitor Convergence**: Always check convergence metrics in production

3. **Tune Thresholds**: Adjust intervention_threshold based on your risk tolerance

4. **Use Verbose Mode**: Enable verbose logging during development

5. **Cache Results**: Large experiments can be expensive; cache intermediate results

## 📖 Example Notebooks

Interactive Jupyter notebooks available in `notebooks/`:

```bash
# Start Jupyter
jupyter notebook

# Open notebooks/quickstart.ipynb
```

Notebooks include:
- `01_basic_usage.ipynb`: Basic framework usage
- `02_vulnerability_analysis.ipynb`: Security analysis
- `03_convergence_analysis.ipynb`: Mathematical analysis
- `04_production_deployment.ipynb`: Deployment guide

## 🆘 Getting Help

- **Documentation**: Check [docs/](docs/)
- **Examples**: Browse [examples/](examples/)
- **Issues**: [GitHub Issues](https://github.com/yourusername/governance-security-by-design/issues)
- **Email**: hj@himanshujoshi.ai

## ✅ Verification Checklist

- [ ] Virtual environment created and activated
- [ ] Package installed (`pip install -e .`)
- [ ] API keys configured in `.env`
- [ ] Test import works: `from governance_framework import GovernanceEngine`
- [ ] Basic example runs successfully
- [ ] Tests pass: `pytest`

You're ready to build safe agentic AI systems! 🎉
