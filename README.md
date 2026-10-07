# RAG Pipeline Analytics & Knowledge Base Monitor

> **Demo on simulated data.** Every number on this dashboard is generated in the browser by a random number generator, so the figures are illustrative. They are not results from real company data or a trained production model. The project shows how the analysis and the interactive visuals work, built as a single HTML file with Plotly.js.

An interactive dashboard for real-time observability into **Retrieval-Augmented Generation (RAG)** systems. Demonstrates deep understanding of embedding spaces, retrieval quality metrics, MCP (Model Context Protocol) integration, and end-to-end RAG pipeline monitoring.

**Live Demo:** [View the Dashboard](https://mayankjoshiii.github.io/rag-analytics-dashboard/)

---

## 🎯 Overview

This dashboard provides comprehensive analytics for RAG systems. It visualizes:

- **Embedding Space Topology** - 2D t-SNE projections showing document clusters and retrieved chunks
- **Retrieval Quality Metrics** - Precision@K, Recall@K, MRR, NDCG across document categories
- **Pipeline Performance** - Latency breakdown, volume funnel, drop-off rates at each stage
- **Answer Quality Analysis** - Relevance vs. quality ratings, faithfulness distributions
- **Token Economics** - Input/output token usage, cost tracking, tokens-per-query trends
- **MCP Integration Monitor** - Tool invocations, latency distributions, resource utilization

Built as a **single static HTML file** with all CSS, JavaScript, and Plotly visualizations embedded—deploy anywhere, no backend required.

---

## 🏗️ RAG Pipeline Architecture

RAG combines the strengths of retrieval systems with generative models:

```
Query Input
    ↓
[Embedding] → Vectorize query into embedding space
    ↓
[Retrieval] → Find K most similar documents using cosine similarity
    ↓
[Reranking] → Reorder by semantic relevance (cross-encoder)
    ↓
[Context Assembly] → Build context window from top chunks
    ↓
[LLM Generation] → Pass context + query to language model
    ↓
[Response] → Return grounded answer with citations
```

### Why RAG Matters

- **Reduces Hallucinations** - Grounds responses in actual knowledge base
- **Enables Knowledge Updates** - Add new documents without retraining
- **Improves Accuracy** - Combines retrieval precision with generation fluency
- **Cost Efficient** - Smaller models work better with good retrieval
- **Transparent Attribution** - Users see which documents informed the answer

---

## 💻 Key Features

### 1. **KPI Dashboard**
- **Total Documents Indexed** - Knowledge base size and growth
- **Queries Processed** - System throughput
- **Avg Retrieval Latency** - Embedding + retrieval speed
- **Avg Relevance Score** - Quality of retrieved chunks
- **Hallucination Rate** - Answer accuracy without retrieval context
- **Answer Accuracy** - End-to-end correctness
- **Chunk Hit Rate** - Success rate of retrieving relevant documents
- **Embedding Dimensions** - Semantic richness (1536D for OpenAI Ada-3)

### 2. **Embedding Space Visualization**
- Interactive 2D scatter plot of document chunks (simulated t-SNE)
- Color-coded by document category (HR, Technical, Product, Legal, Finance)
- Hover to see chunk preview text
- Query visualization showing retrieved chunks and distances
- Reveals document clustering and semantic organization

### 3. **Retrieval Quality Heatmap**
- **Query Category × Document Category matrix** showing average relevance scores
- Diverging color scale (red = low, green = high) for easy interpretation
- Identifies which document types serve which queries well
- Highlights gaps and optimization opportunities

### 4. **Top-K Chunk Ranking**
- Ranked bar chart of top-10 retrieved chunks
- Precision@K, Recall@K, MRR (Mean Reciprocal Rank), NDCG@10
- Threshold visualization (e.g., relevance > 0.5)
- Below-threshold chunks shown in faded colors

### 5. **Cosine Similarity Matrix**
- Pairwise similarity between document categories
- Shows content overlap and complementarity
- Helps identify redundancy or gaps in knowledge base

### 6. **RAG Pipeline Funnel**
- Sankey/funnel visualization of query flow through pipeline
- Volume drops at each stage (e.g., retrieval → reranking → LLM)
- Latency breakdown per stage
- Success rate metrics by stage

### 7. **Answer Quality Analysis**
- **Relevance vs Quality Scatter** - Shows correlation between retrieval and answer quality
- **Faithfulness Distribution** - How well answers stick to retrieved context
- **Box plots by Category** - Quality variance across document types

### 8. **Token Usage & Cost Analytics**
- **Stacked area chart** - Input vs output tokens over time
- **Cost tracking** - Monthly spend with realistic pricing (e.g., GPT-4: $0.03/$0.06 per 1K tokens)
- **Tokens-per-query trend** - Optimization opportunities

### 9. **Query Timeline**
- Daily query volume over 3 months
- Overlay of average relevance score
- Annotated events ("New documentation added", "Model upgraded")
- Reveals temporal patterns and system improvements

### 10. **MCP Integration Monitor**
- **Tools Connected** - Active MCP servers and capabilities
- **Resources Available** - Accessible knowledge base resources
- **Prompts Cached** - Cache hit rates for prompt caching
- **Tool Usage Frequency** - Which MCP tools called most
- **Latency Distribution** - Performance of each tool

### 11. **Query Explorer Table**
- Searchable, filterable table of recent queries
- Columns: Query text, category, top document, relevance, latency, tokens, quality
- Color-coded quality badges (high/medium/low)
- Real-time search filtering

---

## 🔌 MCP (Model Context Protocol) Integration

The dashboard includes comprehensive **MCP monitoring** showing:

### MCP Server Status
- **24 Tools Connected** - Available MCP servers (e.g., fetch-documents, search-embeddings)
- **156 Resources Available** - Accessible knowledge bases, APIs, data sources
- **412 Prompts Cached** - Reusable prompt templates with 87% cache hit rate

### Tool Invocation Tracking
- Timeline of MCP tool calls over the past month
- Most-used tools: `rerank-results`, `generate-response`, `compute-similarity`
- Latency distributions by tool (5-200ms range)

### MCP Workflow
```
LLM Generation
    ↓
[MCP Dispatch] → Find best tool for task
    ↓
[Tool Invocation] → Call external resource (fetch data, compute, etc.)
    ↓
[Result Processing] → Parse and validate tool output
    ↓
[Context Augmentation] → Include tool results in LLM context
    ↓
[Response Generation] → Final response with integrated results
```

---

## 📊 Data Generation & Realism

The dashboard uses **synthetic but realistic data**:

### Documents (200 chunks)
- Pre-projected 2D embeddings with cluster structure
- 5 categories: HR Policies, Technical Docs, Product Specs, Legal, Finance
- Relevance biases reflecting real-world distributions
- Token counts (50-500 tokens per chunk)

### Queries (500 samples)
- Temporal distribution over 90 days
- Relevance follows beta distribution (most queries get decent results, some fail)
- Categories matching document types
- Latencies: 20-150ms (realistic for embedding + retrieval)

### MCP Events (200 invocations)
- 8 tool types with realistic usage patterns
- Latencies: 5-200ms
- Success rate: 95% (5% error for realism)

### Temporal Patterns
- Query volume varies by day (higher mid-week)
- Improvements over time (relevance increases as docs added)
- Realistic cost scaling with token usage

---

## 🛠️ Technology Stack

| Component | Technology |
|-----------|------------|
| **Visualization** | Plotly.js (CDN) |
| **Charts** | Heatmaps, Scatter plots, Bars, Funnels, Box plots |
| **Styling** | CSS Grid, CSS Gradients, Responsive Design |
| **Data** | Seeded random generation (reproducible) |
| **Embedding Projection** | Simulated t-SNE (cluster-preserving random projection) |
| **Deployment** | Single HTML file (static) |

---

## 🚀 Features Implemented

### Computational Features
- ✅ Cosine similarity calculation
- ✅ Simulated t-SNE projection with cluster structure
- ✅ Precision@K, Recall@K, MRR, NDCG computation
- ✅ Token counting estimation
- ✅ Search/filter engine for query explorer
- ✅ Temporal aggregation and trend analysis

### Visualization Features
- ✅ Interactive Plotly charts (hover, zoom, pan)
- ✅ Tab-based navigation for 8 sections
- ✅ Responsive design (mobile, tablet, desktop)
- ✅ Dark theme with gradient accents
- ✅ Color-coded quality indicators
- ✅ Animated KPI cards and status indicators

### UX Features
- ✅ Query selector with live chart updates
- ✅ Search box for query explorer
- ✅ Metrics dynamically update on query selection
- ✅ Smooth transitions and hover effects
- ✅ Mobile-responsive navigation
- ✅ Legend and annotation support

---

## 📈 Key Metrics Explained

### Retrieval Metrics
- **Precision@K** - Of top K results, how many are relevant? (0.85 = 85%)
- **Recall@K** - Of all relevant documents, how many are in top K?
- **MRR (Mean Reciprocal Rank)** - Average rank of first relevant result (0.81 = top 1.2 on average)
- **NDCG@10** - Discounted cumulative gain favoring relevance at top (0.88 = excellent)

### Quality Metrics
- **Hallucination Rate** - % of answers with unsupported claims (3.2%)
- **Faithfulness** - How well answer adheres to retrieved context (0-1 scale)
- **Answer Accuracy** - Verified correctness against ground truth (92.1%)

### Performance Metrics
- **Latency Breakdown** - Time spent in each pipeline stage (embedding, retrieval, LLM)
- **Tokens/Query** - Average tokens consumed (important for cost)
- **Hit Rate** - % of queries returning relevant documents (87.3%)

---

## 🎨 Design System

### Color Palette
```css
--primary: #06b6d4    /* Cyan - primary accent */
--secondary: #a78bfa  /* Violet - secondary accent */
--tertiary: #f472b6   /* Pink - tertiary accent */
--success: #10b981    /* Green - positive metrics */
--warning: #f59e0b    /* Amber - warnings */
--danger: #ef4444     /* Red - errors/negative metrics */
--bg-dark: #0a0a1a    /* Dark background */
--bg-card: #0f0f23    /* Card background */
--text-primary: #f0f0f0 /* Primary text */
--text-secondary: #a0a0b0 /* Secondary text */
```

### Typography
- Headers: 24-32px, bold, gradient text
- Body: 14px, Segoe UI
- Labels: 12px, uppercase, letter-spaced
- Code: Monospace, 13px

### Components
- KPI Cards: Gradient borders, hover lift effect
- Charts: Transparent backgrounds, dark grid lines
- Tables: Alternating row colors, quality badges
- Buttons: Gradient fills, smooth transitions

---

## 📖 How to Use

### 1. **Open the Dashboard**
```bash
# Clone the repository
git clone https://github.com/mayankjoshiii/rag-analytics-dashboard.git
cd rag-analytics-dashboard

# Open in browser (or use Live Server)
open index.html
# or
python -m http.server 8000
# Visit: http://localhost:8000
```

### 2. **Navigate Tabs**
Click tabs at the top to explore different sections:
- **Overview** - KPIs and timeline
- **Embedding Space** - 2D visualization
- **Retrieval Quality** - Heatmaps and metrics
- **Pipeline Funnel** - Funnel analysis
- **Answer Quality** - Quality distributions
- **Token Analytics** - Cost tracking
- **MCP Integration** - Tool monitoring
- **Query Explorer** - Searchable table

### 3. **Interact with Charts**
- **Hover** for detailed values
- **Click legend items** to toggle series
- **Drag to pan**, scroll to zoom
- **Double-click** to reset view

### 4. **Select Queries**
Use dropdowns to select specific queries and see:
- Top-K retrieved chunks
- Precision/Recall/NDCG metrics
- Embedding space with query point and retrieved chunks

### 5. **Search Queries**
Use the search box in Query Explorer to filter by:
- Query text
- Category
- Document retrieved
- Quality rating

---

## 🔍 Understanding the Visualizations

### Embedding Space (Most Important)
- **Clusters** - Documents of same category group together
- **Distance** - Closer points = more similar embeddings
- **Query Point** - Selected query (if implemented)
- **Retrieved Chunks** - Highlighted as connected points
- **Color** - Document category (5 different colors)

**What to Look For:**
- Clear category clustering = good semantic separation
- Evenly distributed = balanced coverage
- Dense regions = redundant content (candidate for pruning)

### Retrieval Heatmap
- **Red cells** - Query category poorly served by document category
- **Green cells** - Strong retrieval performance
- **Diagonal strength** - How well each category self-serves

**Example Interpretation:**
- HR Questions → HR Policies: strong (green)
- HR Questions → Technical Docs: weak (red)

### Pipeline Funnel
- **Width** - Volume of queries at each stage
- **Drop-off** - Failed queries (e.g., 156K → 150K in LLM stage)
- **Stage order** - Visual representation of pipeline flow

**Cost implications:** Wider early stages = higher embedding costs; wider later stages = higher LLM costs.

---

## 🔐 MIT License

```
Copyright (c) 2026 Mayank Joshi

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

---

## 👨‍💼 Author

**Mayank Joshi**
- MSc Business Analytics
- Data Analyst | AI/ML Engineer
- GitHub: [@mayankjoshiii](https://github.com/mayankjoshiii)

---

## 📚 Further Reading

### RAG Papers & Resources
- [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks (Lewis et al., 2020)](https://arxiv.org/abs/2005.11401)
- [REALM: Retrieval-Augmented Language Model Pre-Training](https://arxiv.org/abs/2002.08909)
- [Dense Passage Retrieval for Open-Domain Question Answering](https://arxiv.org/abs/2004.04906)

### Embedding & Similarity
- [BERT: Pre-training of Deep Bidirectional Transformers](https://arxiv.org/abs/1810.04805)
- [Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks](https://arxiv.org/abs/1908.10084)
- [Scaling Laws for Neural Language Models (Chinchilla/Gopher)](https://arxiv.org/abs/2203.15556)

### Evaluation Metrics
- [Precision & Recall in Information Retrieval](https://en.wikipedia.org/wiki/Precision_and_recall)
- [NDCG: Normalized Discounted Cumulative Gain](https://en.wikipedia.org/wiki/Discounted_cumulative_gain)
- [Mean Reciprocal Rank (MRR)](https://en.wikipedia.org/wiki/Mean_reciprocal_rank)

### MCP (Model Context Protocol)
- [Anthropic MCP Spec](https://modelcontextprotocol.io/)
- [MCP Tools & Resources](https://modelcontextprotocol.io/docs/concepts/tools)
- [Prompt Caching for Cost Optimization](https://platform.openai.com/docs/guides/prompt-caching)

---

## 🎓 Why This Matters (2026)

Every company building AI is now implementing RAG systems:

1. **Accuracy** - LLMs are unreliable; RAG adds ground truth
2. **Scale** - Knowledge base grows without retraining models
3. **Cost** - Smaller models work better with good retrieval
4. **Transparency** - Users see citations and source documents
5. **Trust** - Reduced hallucinations = safer deployment

**This dashboard demonstrates:**
- Deep understanding of embedding spaces and semantic similarity
- Ability to design and interpret retrieval quality metrics
- End-to-end observability into AI systems
- MCP integration for extensible architectures
- Production-grade visualization and UX

---

## 🚀 Future Enhancements

- [ ] Real database integration (PostgreSQL + pgvector)
- [ ] Live query processing with actual embeddings
- [ ] Advanced reranking strategies comparison
- [ ] A/B testing framework for retrieval strategies
- [ ] Prompt optimization analytics
- [ ] Custom metric definitions
- [ ] Export/dashboard sharing
- [ ] Alert thresholds for SLOs

---

**Questions? Issues? Improvements?**
Open an issue or reach out at [GitHub Issues](https://github.com/mayankjoshiii/rag-analytics-dashboard/issues)

---

*Built with ❤️ for the AI engineer community. Join the RAG revolution.* 🚀
