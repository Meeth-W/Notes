---

# ✅ **Artificial Intelligence Solved Question Bank**

---

# 📘 **Module 4: Knowledge Representation & Expert Systems**

## 🔹 **2 Marks Questions & Answers**

**1. Define knowledge representation in Artificial Intelligence.**
**Answer:**
Knowledge Representation is the method of structuring and organizing information logically so that an AI agent can understand, reason about, and utilize it to solve complex problems. It bridges raw data and actionable machine intelligence through logical notations and ontologies.

**2. State any one component of an Expert System.**
**Answer:**
**The Inference Engine:** This component acts as the "brain" of the Expert System, processing the rules stored in the Knowledge Base alongside user inputs to deduce new information and formulate logical conclusions or recommendations.

**3. Summarize knowledge acquisition.**
**Answer:**
Knowledge Acquisition is the process of extracting, structuring, and organizing domain-specific expertise from human experts, databases, or documents and transferring it into the Knowledge Base of an Expert System.

---

## 🔹 **5 Marks Questions & Answers**

**4. Compare forward and backward chaining in terms of efficiency and application scenarios.**
**Answer:**
* **Processing Direction:** Forward Chaining is data-driven, starting with known facts and applying rules successively to extract new facts until a goal is reached. Backward Chaining is goal-driven, starting with a hypothesis and working backward to find the supporting facts.
* **Efficiency:** Backward Chaining is typically more efficient for specific diagnostic queries because it only searches paths directly relevant to the target goal. Forward Chaining can be less efficient as it generates all possible conclusions from available data, even irrelevant ones.
* **Application Scenarios:** 
  - *Forward Chaining* is best suited for planning, monitoring, and broad synthesis tasks (e.g., configuring a computer system based on parts, monitoring system states).
  - *Backward Chaining* is ideal for diagnostics, troubleshooting, and targeted classification tasks (e.g., medical diagnosis, debugging code limits).

**5. Design a PROLOG program to represent family relationships and justify the logical rules used.**
**Answer:**
**Program:**
```prolog
% Facts
parent(john, mary).
parent(john, alex).
parent(mary, susan).
male(john).
male(alex).
female(mary).
female(susan).

% Rules
father(X, Y) :- parent(X, Y), male(X).
mother(X, Y) :- parent(X, Y), female(X).
sibling(X, Y) :- parent(Z, X), parent(Z, Y), X \= Y.
grandparent(X, Y) :- parent(X, Z), parent(Z, Y).
```
**Justification:**
The facts declare direct foundational truths (John is a parent of Mary, John is male). The rules apply logical inference dynamically. For example, the `father(X, Y)` rule states `X is the father of Y IF X is a parent of Y AND X is male`. The `sibling` rule guarantees that two distinct individuals sharing a common parent `Z` are identified as siblings, using `X \= Y` to prevent the agent from assuming an entity is its own sibling.

**6. Evaluate the effectiveness of Expert Systems in real-world decision-making scenarios.**
**Answer:**
Expert Systems simulate human expertise deeply by structuring isolated domain logic into rigid rules. 
* **Strengths:** They offer extreme consistency, eliminating human fatigue and bias. In fields like medical diagnosis (e.g., MYCIN) or mineral exploration (PROSPECTOR), they can rapidly process thousands of variables to offer highly reliable output.
* **Limitations:** They suffer from the "knowledge acquisition bottleneck" (harvesting human logic is difficult) and lack common sense reasoning. If faced with edge cases outside their programmed rules, they experience "brittle failure" instead of graceful degradation. Overall, they are highly effective in narrow, well-defined domains but fail in dynamic, generalized environments.

**7. Differentiate between propositional logic and predicate logic.**
**Answer:**
* **Granularity & Expressiveness:** Propositional Logic evaluates complete declarative sentences (propositions) that are strictly True or False (e.g., "P = It is raining"). It cannot inspect the internal structure. First-Order Predicate Logic breaks propositions into objects, properties, and relations, offering massive expressive depth (e.g., "Rain(x)").
* **Quantification:** Propositional Logic lacks quantifiers entirely. Predicate Logic introduces Universal ($\forall$) and Existential ($\exists$) quantifiers, enabling statements like "All humans are mortal" ($\forall x (Human(x) \rightarrow Mortal(x))$).
* **Complexity:** Predicate logic features significantly higher computational complexity because it handles dynamic variables and relations, whereas propositional calculus relies strictly on mechanical truth tables.

**8. Discuss the importance of logical consistency in knowledge representation.**
**Answer:**
Logical consistency guarantees that a Knowledge Base does not contain contradictory facts or rules. 
* **Preventing System Collapse:** If contradictions exist (e.g., $P \land \neg P$), classical logic enables the system to infer literally any conclusion (the Principle of Explosion). This destroys the engine's reliability.
* **Deterministic Inference:** Consistent representation ensures the Inference Engine can reliably navigate resolution theorem proving without looping infinitely or freezing.
* **User Trust:** In applications like medical diagnosis or financial auditing, an inconsistent system dispensing conflicting advice rapidly destroys user trust and system validity.

---

## 🔹 **Additional Important Questions & Answers**

**9. Explain the concept of Resolution in Propositional Logic.**
**Answer:**
Resolution is a powerful inference rule yielding a complete resolution theorem-proving algorithm.
*   **Mechanism:** It operates by taking two clauses containing complementary literals (one positive, one negative) and producing a new clause containing all the literals of the two original clauses except the complementary ones. If $A \lor B$ and $\neg B \lor C$ are true, we resolve them to conclude $A \lor C$.
*   **Proof by Contradiction:** Resolution is often implemented using proof by contradiction. To prove a goal theorem, its negation is added to the Knowledge Base. If applying resolution subsequently reduces the facts down to an empty clause (a clear contradiction), the original goal theorem is mathematically proven true.

**10. Describe the WUMPUS WORLD Environment and its significance in building a Knowledge-Based Agent.**
**Answer:**
The Wumpus World is a classical grid-based environment acting as a foundational benchmark test for Knowledge-Based Agents.
*   **Structure:** The agent navigates a dark cave network. Its goals are discovering gold, surviving bottomless pits, and escaping a deadly Wumpus beast.
*   **PEAS Layout:** It relies on sensors (Stench for Wumpus, Breeze for Pits, Glitter for Gold) and performs actions (Move, Shoot, Grab, Climb). 
*   **Significance:** It forces developers to implement rigorous First-Order Logic because the agent cannot see the entire grid map inherently. The agent must logically deduce safe squares using adjacent sensory percepts explicitly without guessing, demonstrating the critical supremacy of rigorous Knowledge Representation during uncertainty.

---

# 📘 **Module 5: Machine Learning & Applications**

## 🔹 **2 Marks Questions & Answers**

**1. State one application of AI in healthcare.**
**Answer:**
**Medical Imaging Analysis:** AI models (especially Convolutional Neural Networks) are used to scan X-Rays and MRIs to rapidly detect tumors and anomalies, significantly assisting radiologist diagnostic accuracy.

**2. Mention one ethical issue in AI development.**
**Answer:**
**Algorithmic Bias:** AI systems trained on historically prejudiced datasets inherently learn and perpetuate those biases, frequently resulting in skewed or racially/gender-biased conclusions in critical sectors like loan approvals or criminal justice.

---

## 🔹 **5 Marks Questions & Answers**

**3. Explain how Decision Trees are used in recommendation systems.**
**Answer:**
Decision Trees operate by partitioning data structurally across internal nodes mapping distinct feature queries.
*   **Recommendation Mapping:** When calculating recommendations, the algorithm evaluates user preferences (e.g., "Age > 20?", "Action Movie Fan?"). 
*   **Execution:** Each node strictly splits users down a branch based on boolean testing until a terminal leaf node is reached. This leaf node holds the final recommendation output (e.g., "Recommend Matrix").
*   **Advantage:** They offer unparalleled system explainability (White-Box model). Engineers can transparently trace back the exact logical branch parameters explaining *why* the system recommended a specific item to an end-user.

**4. Analyze industry applications of AI and discuss their societal impact and ethical implications.**
**Answer:**
*   **Industry Applications:** AI aggressively dominates Finance (algorithmic trading & anomaly fraud detection), Logistics (predictive maintenance & automated routing), and Customer Service (advanced NLP LLM chatbots mapping instant support resolutions).
*   **Societal Impact:** The operational efficiency gain is massive, dropping corporate overhead dramatically while offering consumers hyper-personalized digital experiences globally.
*   **Ethical Implications:** The transition creates highly severe ethical frictions, including drastic human displacement (job loss due to automation), black-box AI logic limiting system accountability during catastrophic failures, and immense privacy erosion due to mass-data harvesting required to continually train these vast neural networks continuously.

---

## 🔹 **Additional Important Questions & Answers**

**5. Describe how a Tic-Tac-Toe Game Agent works and discuss its search methodology.**
**Answer:**
A Tic-Tac-Toe Game Agent calculates its moves comprehensively using Adversarial Search mechanisms via the **Min-Max Algorithm**.
*   **Search Tree Generation:** The agent conceptually creates a game tree mapping all possible future board states stemming from the current position.
*   **Min-Max Concept:** It assumes the opponent plays perfectly to minimize the agent's score. The agent itself attempts to maximize the ultimate score.
*   **Execution:** By recursively evaluating the terminal utility states (Win=+1, Loss=-1, Draw=0) and backing up the values to the root, the agent flawlessly discovers the optimal immediate move mathematically guaranteeing at least a draw against any player.

**6. Discuss the methodology and benefits of building a Chatbot using Intelligent Agents.**
**Answer:**
*   **Methodology:** Intelligent Chatbots utilize Natural Language Processing (NLP) modules to tokenize and contextualize raw user input. They map the intent using classification algorithms and process the query via a centralized Knowledge Base or LLM API framework, formulating structured dynamic responses natively.
*   **Benefits:** These Agents guarantee immediate 24/7 global accessibility, eliminating waiting queues entirely. They drastically scale business operations without linearly increasing human workforce costs while dynamically personalizing recommendations utilizing deep historical user-interaction logs continuously.

**7. Explain how the Maze Solver utilizes DFS and BFS concepts.**
**Answer:**
Maze Solving Agents systematically parse grid environments searching for optimal escape paths.
*   **Depth First Search (DFS):** The algorithm aggressively plunges down a single directional pathway until it physically hits a dead end, subsequently backtracking. It demands minimal memory but frequently generates heavily unoptimized, chaotic escape routes.
*   **Breadth First Search (BFS):** This mechanism incrementally explores all surrounding adjacent grid spots simultaneously sequentially radiating outward. While it aggressively consumes vast amounts of system memory tracking all node layers, it structurally guarantees uncovering the absolute shortest path directly mathematically.

---

# 📘 **Module 6: Deep Learning, NLP & Generative AI**

## 🔹 **2 Marks Questions & Answers**

**1. Define Generative AI.**
**Answer:**
Generative AI refers to advanced machine learning models (often built on Transformer architectures or GANs) expressly designed to synthesize entirely novel, high-quality content—including text, imagery, music, and synthetic data—mimicking human creative patterns.

**2. Define Transformer architecture.**
**Answer:**
The Transformer is a deeply parallelized neural network architecture completely abandoning sequential processing in favor of a Self-Attention mechanism, allowing it to evaluate the overarching relational context of all data sequence tokens simultaneously.

**3. Define the Encoder–Decoder model.**
**Answer:**
The Encoder-Decoder model separates processing tasks: the Encoder aggressively compresses an input sequence into a dense latent context vector mapping its meaning, and the Decoder sequentially unravels that vector to generate a completely new output sequence (often in a different format or language).

---

## 🔹 **5 Marks Questions & Answers**

**4. Examine Self-Attention with a suitable example.**
**Answer:**
Self-Attention mathematically calculates how heavily distinct words inside a singular sentence recursively relate to one another dynamically, mapping contextual weights independently of their physical distance.
*   **Example Context:** The sentence "The bank of the river" vs "The bank approved the loan".
*   **Mechanism Execution:** While old models process the word "bank" statically, Self-Attention checks surrounding tokens simultaneously. In sentence one, it identifies strong correlations with "river", outputting a geographical representation. In sentence two, it ties strongly to "loan", shifting the representation vector fully to a financial context seamlessly.

**5. Differentiate between BERT and GPT.**
**Answer:**
*   **Architecture Flow:** BERT (Bidirectional Encoder Representations from Transformers) leverages an **Encoder-Only** architecture. It reads the entire text sequence bidirectionally (left-to-right and right-to-left simultaneously) mapping deep context natively. GPT (Generative Pre-trained Transformer) leverages a **Decoder-Only** structure, processing tokens exclusively unidirectionally (left-to-right).
*   **Primary Application Tasks:** Because BERT natively understands bidirectional context organically, it dominates classification, sentiment analysis, and question-answering tasks optimally. GPT, relying on unilateral next-token prediction mathematics, excels natively in dynamic generative tasks like automated essay writing and conversational chatbots.

**6. Explore the Encoder–Decoder architecture in Transformers.**
**Answer:**
The standard Transformer operates utilizing specialized interlocking mechanisms:
*   **The Encoder Block:** Responsible purely for absorbing input tokens. It utilizes multi-head self-attention and dense feed-forward networks to distill complex structural relationships into abstract matrix representations independently.
*   **The Decoder Block:** Responsible natively for generation. It features standard self-attention but adds **Cross-Attention** layers that physically connect to the Encoder's final output, forcing the Decoder generation algorithms to pay close attention specifically to the core context constraints defined originally by the input.

**7. Analyze the differences between Encoder-only, Decoder-only, and Encoder–Decoder models.**
**Answer:**
*   **Encoder-Only (e.g., BERT):** Specializes in deeply analyzing input for comprehension. Extremely powerful regarding sentiment analysis or extracting data organically because it maps forward and backward token relations perfectly. It cannot generate output fluidly.
*   **Decoder-Only (e.g., GPT):** Specializes exclusively in recursive sequence generation. It looks strictly at past tokens to continually predict the next logical token linearly. Cannot look 'forward' at ungenerated input.
*   **Encoder–Decoder (e.g., T5, BART):** Combines both paradigms structurally. Best utilized for dynamic transformation tasks where understanding rigid input is necessary before completely regenerating it differently (e.g., Text Summarization, translating raw French to perfect English).

**8. Discuss future trends in deep learning and machine learning and evaluate their impact on industry transformation.**
**Answer:**
*   **Future Trends:** Core trends include the massive acceleration of Multi-Modal AI (models natively synthesizing video, audio, and text simultaneously seamlessly), Edge AI (embedding complex inference logic directly inside localized IoT hardware omitting cloud latency), and Agentic AI (systems capable of autonomous chained task execution without human micro-management).
*   **Industry Transformation:** The impact equates directly to a structural industrial revolution. Heavy industries will become heavily predictive (preventing hardware failures automatically), white-collar analysis jobs will transition into AI oversight management roles, and medical research timelines regarding protein-folding and drug discovery will compress geometrically. 

---

## 🔹 **10 Marks Questions & Answers**

**9. Design a Transformer-based solution for multilingual translation and justify the architecture used.**
**Answer:**
**System Design Architecture:**
For a scalable Multilingual Translation system, an **Encoder-Decoder Transformer Architecture** framework is mandatory.
1.  **Tokenization Engine:** Deploy a Byte-Pair Encoding (BPE) sub-word tokenizer natively handling massive vocabulary intersections spanning diverse alphabetic languages.
2.  **Encoder Pathway (The Source Analyzer):** The system passes target foreign sentences through massive Multi-Head Self Attention matrices mapping bidirectional context deeply (e.g., handling German verb placements perfectly).
3.  **Cross-Attention Bottleneck:** The context vector bridges the models; translating conceptual meaning purely separated from language-specific grammar.
4.  **Decoder Pathway (The Generator):** It actively predicts the target language sequence dynamically matching the Encoder's conceptual vector using Auto-regressive Masked Attention logic.

**Justification for Approach:**
Standard RNN models suffer catastrophically regarding vanishing gradients over long sentences, actively “forgetting” the beginning of paragraphs natively. The Transformer architecture is justified fully because its Self-Attention mechanism mathematically evaluates long-range context dependencies instantaneously in parallel. Using the Encoder-Decoder configuration specifically natively allows the model to map the complex semantic structure inside the Encoder before generating grammatically complex new sequences linearly inside the Decoder.

---

## 🔹 **Additional Important Questions & Answers**

**10. Explain the concept of Agentic AI and its rising influence in generative task execution.**
**Answer:**
*   **Core Concept:** Unlike standard Generative AI (which requires explicit human prompts to generate static output), Agentic AI intrinsically acts as an autonomous systemic operator. It evaluates a high-level goal, autonomously breaks that goal down into sequential sub-tasks, utilizes external digital tools (like web browsers or API endpoints), and corrects its own logic automatically via iterative feedback loops executing the long-term objective organically.
*   **Rising Influence:** Its massive influence stems from reducing human bottleneck interaction completely. Instead of a developer individually prompting a model to write code, debug the code, and push the code consecutively—an Agentic AI system handles the entire cyclical execution pipeline instantly independently.

**11. Discuss Machine translation using transfer learning with pre-trained models.**
**Answer:**
*   **The Problem:** Training translation systems entirely from scratch requires petabytes of localized language data alongside monstrous computing power. Standard low-resource languages (e.g., Swahili, Marathi) lack sufficient internet data to accommodate raw training correctly.
*   **Transfer Learning Solution:** Engineers utilize large pre-trained Foundation Models (which already possess profound structural understandings regarding linguistic grammar and contextual semantics algorithmically). 
*   **Fine-Tuning:** By freezing the overarching core model parameters and specifically fine-tuning the outer layers using a highly targeted comparative dataset covering the exact target language natively, the system essentially "transfers" generic language comprehension directly toward a niche linguistic translation task. This drastically slashes computational overhead while exponentially increasing output quality across rare languages.

---

> **End of Artificial Intelligence Solved Question Bank**
