---
layout: post
title:  "Notes on the Theory of Computation"
date:   2020-12-18 23:50:00 -0500
author: Siberian Tiger
categories: math
---

**Table of contents**

- [1 Automata and Language Theory](#1-automata-and-language-theory)
  - [1.1 Regular languages](#11-regular-languages)
    - [1.1.1 Finite automata](#111-finite-automata)
    - [1.1.2 Nondeterminism](#112-nondeterminism)
    - [1.1.3 Regular expressions](#113-regular-expressions)
    - [1.1.4 Nonregular languages](#114-nonregular-languages)
  - [1.2 Context-free languages](#12-context-free-languages)
    - [1.2.1 Context-free grammars (CFGs)](#121-context-free-grammars-cfgs)
    - [1.2.2 Pushdown automata](#122-pushdown-automata)
    - [1.2.3 Non-context-free languages](#123-non-context-free-languages)
- [2 Computability Theory](#2-computability-theory)
  - [2.1 The Church-Turing Thesis](#21-the-church-turing-thesis)
    - [2.1.1 Turing machines](#211-turing-machines)
    - [2.1.2 Variants of Turing machines](#212-variants-of-turing-machines)
    - [2.1.3 The definition of algorithms](#213-the-definition-of-algorithms)
  - [2.2 Decidability](#22-decidability)
    - [2.2.1 Decidable languages](#221-decidable-languages)
    - [2.2.2 Undecidability](#222-undecidability)
  - [2.3 Reducibility](#23-reducibility)
    - [2.3.1 Undecidable problems](#231-undecidable-problems)
    - [2.3.2 Mapping reducibility](#232-mapping-reducibility)
  - [2.4 Advanced topics in Computability Theory](#24-advanced-topics-in-computability-theory)
    - [2.4.1 The recursion theorem](#241-the-recursion-theorem)
    - [2.4.2 Introduction to mathematical logic](#242-introduction-to-mathematical-logic)
- [3 Complexity Theory](#3-complexity-theory)
  - [3.1 Time complexity](#31-time-complexity)
    - [3.1.1 The Class P](#311-the-class-p)
    - [3.1.2 The Class NP](#312-the-class-np)
  - [3.2 Space complexity](#32-space-complexity)
    - [3.2.1 PSPACE and NPSPACE](#321-pspace-and-npspace)
    - [3.2.2 Savitch's theorem](#322-savitchs-theorem)
    - [3.2.3 PSPACE-completeness](#323-pspace-completeness)
    - [3.2.4 Log space](#324-log-space)
  - [3.3 Intractability](#33-intractability)
    - [3.3.1 Hierarchy theorems](#331-hierarchy-theorems)
    - [3.3.2 Oracles](#332-oracles)
  - [3.4 Advanced topics in Complexity Theory](#34-advanced-topics-in-complexity-theory)
    - [3.4.1 Probabilistic algorithms](#341-probabilistic-algorithms)
    - [3.4.2 Interactive proof systems](#342-interactive-proof-systems)

------

This post is based on a course that I took in fall, 2020. 
I refine it aperiodically for the purpose of summarizing and promoting my understanding.

## 1 Automata and Language Theory

### 1.1 Regular languages

#### 1.1.1 Finite automata

Schematic diagram.

A *finite automaton* $M$ is a quintuple $(Q, \Sigma, \delta, q_0, F)$, where $Q$ is a finite set of states, $\Sigma$ is a finite set of alphabet symbols, $\delta: Q\times \Sigma \to Q$ is the transition function, $q_0$ is the start state and $F$ is the set of accept states.

A *string* is a finite sequence of symbols in $\Sigma$. A *language* is a finite/infinite set of strings. The empty string is denoted by $\epsilon$, and the empty language by $\emptyset$.

Define $L(M)$ to the set of strings accepted by $M$. $L(M)$ is said to be the language of $M$, or $M$ recognizes $L(M)$. A language is *regular* if some finite automaton recognizes it.

*Regular operations:* ($A$ and $B$ are languages)
- Union: $A\cup B = \{w: w\in A \text{ or } w\in B\}$;
- Concatenation: $A\circ B = \{xy: x\in A \text{ and } y\in B \}$ or $AB$;
- Star $A^{\ast} = \{x_1\cdots x_k: k\ge 0, \text{ and } x_i\in A \text{ for all } i\in [k]\}$. $\epsilon \in A^{\ast}$ always.

#### 1.1.2 Nondeterminism

Nondeterministic finite automata have three new features:
- Allow multiple paths (0 - path vanishes, 1 or many at each step);
- Allow "free" moves without reading input by $\epsilon$-transition(caveat: some branches may loop);
- Accept an input if some path leads to an accept state.

Note that nondeterminism does not correspond to a physical machine that we can build. However, it is useful mathematically.

Formally, a *nondeterministic finite automaton (NFA)* $N$ is a quintuple $(Q, \Sigma, \delta, q_0, F)$. Here $\delta: Q\times \Sigma_{\epsilon} \to \mathcal{P}(Q)$, where $\Sigma_{\epsilon} = \Sigma \cup \{\epsilon\}$ and $\mathcal{P}= \{R: R\subset Q\}$ is the power set.

Three ways to think about nondeterminism:
- Computational: fork parallel threads (caveat: the threads cannot merge);
- Mathematical: tree with branches;
- Magical: guess at each nondeterministic step which way to go. The machine always makes the right guess that leads to accepting, if possible.

Theorem. If an NFA recognizes $A$ then $A$ is regular. Proof. For NFA $M$, construct DFA $M'$ that keeps track of the subset of possible states in $M$. Concretely, let $Q' = \mathcal{P}(Q)$.

Theorem (closure properties for regular languages). The set of regular
languages is closed under $\cup, \circ, \ast$. Proof.
- Let $M_1$ recognize $A_1$ and let $M_2$ recognize $A_2$. Show $A_1 \cup A_2$ is regular by either coupling $M_1, M_2$ or contructing an NFA with $\epsilon$-transition at the start.
- Show $A_1 A_2$ is regular by adding $\epsilon$-transition at the end of $M_1$ to the start state of $M_2$.
- Let $M$ recognize $A$. Show $A$ is regular by adding $\epsilon$-transition from accept states to the start state. To accommodate $\epsilon \in A^{\ast}$, add an accept state with $\epsilon$-transition to the start state.

#### 1.1.3 Regular expressions

A *regular expression* is a string built from $\Sigma$, members of $\Sigma$, $\emptyset$, $\epsilon$ by using $\cup, \circ, \ast$.

Theorem. If $R$ is a regular expression and $A = L(R)$ then $A$ is regular. Proof. Contruct an NFA $M$ for atomic $R$ and leave the rest to the closure property.

A *generalized NFA (GNFA)* allows regular expressions as transition labels.

Lemma. Every GNFA $G$ has an equivalent regular expression $R$. Proof. Convert the GNFA to a special form with one accept state (distinct from the start state) and one arrow from each state to each state. Apply induction to the number of states $k$ of $G$. The induction step converts a $k$-state GNFA to an equivalent $(k-1)$-state GNFA.

Theorem. If $A$ is regular then $A = L(R)$ for some regular expression $R$. Proof. A DFA is a special case of GNFA.

#### 1.1.4 Nonregular languages

Pumping lemma. For every regular language $A$, there is a number $p$ (the pumping length) such that for every $s\in A$ and $|s| > p$ then $s = xyz$ where 1) $xy^iz\in A$ for all $i\ge 0$, and notably $i$ can be zero; 2) $y\neq \epsilon$; 3) $|xy|\le p$. Proof. Let $p$ be the number of states in DFA $M$. Then for any string $s$, let $y$ be the substring between two repetitions (guaranteed by the pigeonhold principle) of the same symbol.

Example 1. $D = \{ 0^k1^k: k\ge 0 \}$ is nonregular. Proof. Consider $s = 0^p1^p$.

Example 2. $F = \{ ww: w\in \Sigma^{\ast} \}$ is nonregular. Say $\Sigma = \{0, 1\}$. Proof. Consider $s = 0^p 1 0^p 1$.

Example 3 (combine closure properties with the pumping lemma).
$B = \{w: w \text{ has equal numbers of $0$s and $1$s}\}$ is nonregular.
Proof: by contradiction. If $B$ is regular then $B\cap 0^{\ast} 1^{\ast}$ is regular, which is Example 1 in this section.

### 1.2 Context-free languages

#### 1.2.1 Context-free grammars (CFGs)

Grammar $G$ generates strings: 1) Write down the start variable. 2) Replace any variable according to a rule; repeat until only terminals remain. The result is a generated string. $L(G)$ is the language of all generated strings. We call $L(G)$ a *context-free language (CFL)*.

A *CFG* $G$ is a quadruple $(V, \Sigma, R, S)$, where $V$ is a finite set of variables, $\Sigma$ is a finite set of terminals, $R$ is a finite set of rules $V \to (V\cup \Sigma)^{\ast}$, $S$ is a start variable.

$u$ yields $v$ if $u$ to $v$ with one substitution step: $u \Rightarrow v$. $u$ derives $v$ if $u$ to $v$ with some number of substitution steps: $u \stackrel{\ast}{\Rightarrow} v$. $u$ derives itself. Formally, $L(G) = \{ w\in \Sigma^{\ast}: S \stackrel{\ast}{\Rightarrow} w \}$.

If a string has two different parse trees then it is derived ambiguously and we say that the grammar is *ambiguous*.

**Chomsky normal form (CNF)**. Every rule is of the form $A\to BC$, $A\to a$, $S\to \epsilon$ where $a$ is any terminal, $A, B, C$ are variables, $B, C$ are not the start variables.

Theorem. Any CFL is generated by a CFG in Chomsky normal form. 
Proof. Convert a CFG to an equivalent CNF.

Theorem. If $G$ is a CFG in CNF, then for any string $w\in L(G)$ of length $n\ge 1$, exactly $2n-1$ steps are required for any derivation of $w$. Proof.

#### 1.2.2 Pushdown automata

A *pushdown automaton (PDA)* is a hextuple $(Q, \Sigma, \Gamma, \delta, q_0, F)$, where $Q$ is a finite set of states, $\Sigma$ is the input alphabet, $\Gamma$ is the stack alphabet, $\delta: Q\times \Sigma_{\epsilon} \times \Gamma_{\epsilon} \to \mathcal{P}(Q\times \Gamma_{\epsilon})$ is the transition. The nondeterministic forks replicate the stack. A PDA accepts only at the end of input.

(Nondeterministic) PDAs are strictly more powerful than deterministic PDAs.

Note that PDAs may not halt due to the nondeterminism, as in the case of NFAs.

Theorem. $A$ is a CFL if and only if some PDA recognizes it. Proof. \"Only if\": Convert the CFG of $A$ to a PDA by guessing the
substitution in the stack. The other direction is not discussed here.

Corollary. Every regular language is a CFL.

**Closure properties of CFLs.**

Theorem. CFLs are closed under regular operations (union, concatenation, star). Proof.

Theorem. The intersection of a CFL and a regular language is a CFL. 
Proof. $A$ is a CGL and $B$ is regular. When reading the input, the finite control of the PDA for $A$ simulates the DFA for $B$.

If $A, B$ are CGLs then $A\cap B$ may not be a CFL. 
Proof. $A_1 = \{ 0^k 1^k 2^l: k, l\ge 0 \}$ and $A_2 = \{0^l 1^k 2^k: k, l\ge 0\}$ are CFLs, but $A_1 \cap A_2$ is not a CFL.

#### 1.2.3 Non-context-free languages

Pumping lemma for CFLs. For every CFL $A$, there is a $p$ such that if $s\in A$ and $|s| \ge p$ then $s = uvxyz$ where 1) $uv^ixy^iz \in A$ for all $i\ge 0$, 2) $vy \neq \epsilon$, 3) $|vxy| \le p$. 
Proof. Let $b$ be the length of the longest RHS of a rule. Then let $p = b^{|V|} + 1$. The height of the parse tree $h > |V|$, so some variable must repeat on a path.

Example 1. $B = \{0^k 1^k 2^k: k\ge 0\}$ is not a CFL. Proof. Consider $s = 0^p 1^p 2^p$.

Example 2. $F = \{ww: w\in \Sigma^{\ast}\}$ is not a CFL. Proof. Consider $0^p 1^p 0^p 1^p$.

## 2 Computability Theory

### 2.1 The Church-Turing Thesis

#### 2.1.1 Turing machines

Turing machine:
- Head can read and write.
- Head is two-way (can move left or right).
- Tape is infinite (to the right).
- Infinitely many blanks $\sqcup$ following input.
- Can accept or reject at any time (not only at the end of input).

Example. Recognize $a^k b^k c^k$ by erasing single $a, b, c$. The erasing effect is achieved by including $\cancel{a}, \cancel{b}, \cancel{c}$ in the tape alphabet $\Gamma$.

A *Turing machine* is a septuple $(Q, \Sigma, \Gamma, \delta, q_0, q_{acc}, q_{rej})$, where $Q$ is the set of states, $\Sigma$ is the input alphabet not containing the blank symbol $\sqcup$, $\Gamma$ is the tape alphabet with $\sqcup\in \Gamma$ and $\Sigma \subset \Gamma$, $\delta: Q\times \Gamma \to Q \times \Gamma \times \{L, R\}$ is the transition function, $q_0$ is the start state, $q_{acc}$ is the accept state, and $q_{rej} \neq q_{acc}$ is the reject state.

3 possible outcomes for each input $w$: 1) Accept $w$ (enter $q_{acc}$); 2) Reject $w$ by halting (enter $q_{rej}$); 3)  Rejecting $w$ by looping (running forever).

A *configuration* of a TM is its current state $q$, the current tape content $t$, and the current head location $p$. Start configuration, accepting configuration, rejecting configuration. Accepting and rejecting configurations are halting configurations.

Let $M$ be a TM. Then $L(M) = \{w: M \text{ accepts } w\}$. $M$ recognizes $A$ if $A = L(M)$. $A$ is *T-recognizable* if $A = L(M)$ for some TM $M$. TM $M$ is a *decider* if $M$ halts on all inputs. $A$ is *T-decidable* if $A = L(M)$ for some TM decider $M$.

#### 2.1.2 Variants of Turing machines

**Multi-tape Turing machines.**

A *multi-tape TM* includes an input tape and some initially blank working tapes.

Theorem. $A$ is T-recognizable if and only if some multi-tape TM recognizes $A$. Proof. The forward direction is immediate. For the backward direction, convert a multi-tape TM to a single-tape TM by storing the contents of multiple tapes on a single tape in blocks.

**Nondeterministic Turing machines.**

A *nondeterministic Turing machine (NTM)* is similar to a deterministic TM except for its transition function $\delta: Q \times \Gamma \to \mathcal{P}(Q\times \Gamma \times \{L, R\})$.

Theorem. $A$ is T-recognizable if and only if some NTM recognizes $A$.
Proof. The forward direction is immediate. For the backward direction, convert an NTM to a TM by storing threads in blocks.

NTM decider: all branches halt.

Theorem. $A$ is T-decidable if and only if some NTM decides $A$. 
Proof. By the equivalence of TMs and NTMs shown in the proof above.

**Turing enumerators.**

A *Turing enumerator* is a deterministic TM with a printer. It starts on a blank tape and it can print strings $w_1, w_2, \cdots$ possibly going forever (an infinite list of strings). The language is the set of all strings it prints. It is a generator, not a recognizer. For enumerator $E$ we say $L(E) = \{ w: E \text{ prints } w \}$. It may generate the strings of the language in any order, possibly with repetitions.

Theorem. $A$ is T-recognizable if and only if $A = L(E)$ for some T-enumerator $E$. 
Proof. 
$\Rightarrow$: simulate $M$ on each $w_1, \cdots, w_i\in \Sigma^{\ast}$ for $i$ steps and print thoses accepted strings. (Note: the printed strings are not in string order.) 
$\Leftarrow$: on input $w$, run $E$ and every time $E$ outputs a string, compare it with $w$.

Theorem. $A$ is T-decidable if and only if some T-enumerator enumerates $A$ in string order. Proof. $\Rightarrow$: direct. $\Leftarrow$: on input $w$, enumerate $A$ in string order and compare each output with $w$.

#### 2.1.3 The definition of algorithms

**The Church-Turing Thesis.**

TMs are equivalent to algorithms.

**Notation for encodings.**

If $O$ is some object, then let $\langle O \rangle$ denote the encoding of $O$ as a string. If $O_1, \cdots, O_k$ is a list of objects, then let $\langle O_1, \cdots, O_k \rangle$ denote the encoding of them together as a string.

### 2.2 Decidability

#### 2.2.1 Decidable languages

Acceptance problem for DFAs/NFAs. Let $A_{DFA} = \{ \langle B, w \rangle: B \text{ is a DFA and } B \text{ accepts } w \}$.

$A_{DFA}$ is decidable. Proof. Simulate the computation of $B$ on $w$.

$A_{NFA}$ is decidable. Proof. Convert the NFA to a DFA first.

Emptiness problem for DFAs. $E_{DFA}$ is decidable. 
Proof. Check for a path from the start state to an accept state by marking the states reachable from the start states.

Equivalence problem for DFAs. $EQ_{DFA}$ is decidable. 
Proof. Construct a DFA $C$ that recognizes the *symmetric difference* of the languages of $A$ and $B$, i.e., $L(C) = (L(A) \cap \overline{L(B)}) \cup (\overline{L(A)} \cap L(B))$, and run the decider for $E_{DFA}$ on $\langle C \rangle$.

The equivalence problem of regular expressions $EQ_{REX}$ is also decidable, since we can use a TM to convert regular expressions to DFAs.

Acceptance problem for CFGs. $A_{CFG}$ is decidable. Proof. Recall the two lemmas about the Chomsky normal form (CNF). On input $\langle G, w \rangle$, convert $G$ into CNF and try all derivations of length $2|w| - 1$.

As a corollary, every CFL is decidable.

Emptiness problem for CFGs. $E_{CFG}$ is decidable. Proof. Track
backward from terminals to see if the start variable is marked.

Decidable languages are closed under regular operations, complementation, and intersection.

#### 2.2.2 Undecidability

$A_{TM}$ is T-recognizable. Proof. Immediate.

Sets $A$ and $B$ have the same size if there is a 1-1 correspondence (1-1 and onto function) $f: A \to B$. A set is countable if it is finite or it has the same size as $\mathbb{N}$.

$\mathbb{R}$ is uncountable. Proof. Diagonalization.

Corollary. Let $\mathcal{L}$ denote all languages. Then $\mathcal{L}$ is uncountable. Proof. There is a 1-1 correspondence from $\mathcal{L}$ to $\mathbb{R}$.

The set of all TMs is countable. Proof. $\Sigma^{\ast}$ is countable, and $\{\langle M \rangle: M \text{ is a TM } \} \subset \Sigma^{\ast}$.

$A_{TM}$ is not decidable. Proof. Diagonalization. Construct $D$ that on input $\langle M \rangle$ accepts if $M$ rejects $\langle M \rangle$ (known from decider for $A_{TM}$).

Theorem. If $A$ and $\overline{A}$ are T-recognizable then $A$ is decidable. Proof. Run the recognizers of them in parallel.

Corollary. $\overline{A_{TM}}$ is T-unrecognizable. Proof. $A_{TM}$ is T-recognizable but also undecidable.

T-recognizable languages are closed under regular operations and intersection, but not complementation.

### 2.3 Reducibility

#### 2.3.1 Undecidable problems

The reducibility method. Use our knowledge that $A_{TM}$ is undecidable to show other problems are undecidable.

$HALT_{TM}$ is undecidable. Proof. Reduce $A_{TM}$ to $HALT_{TM}$.

$E_{TM}$ is undecidable. Proof. Reduce $A_{TM}$ to $E_{TM}$.

$REGULAR_{TM}$ is undecidable. Proof. Reduce $A_{TM}$ to $REGULAR_{TM}$.

$EQ_{TM}$ is undecidable. Proof. Reduce $E_{TM}$ to $EQ_{TM}$.

**The computation history method for proving undecidability.**

An *(accepting) computation history* for TM $M$ on input $w$ is a sequence of configurations $C_1, \cdots, C_{acc}$ that $M$ enters until it accepts.

A *linearly bounded automaton (LBA)* is a $1$-tape TM that cannot move its head off the input portion of the tape.

$A_{LBA}$ is decidable. Proof. There are finite distinct configurations of an LBA.

$E_{LBA}$ is undecidable. Proof. Reduce $A_{TM}$ to $E_{LBA}$ by the computation history method.

$ALL_{CFG}$ is undecidable. Proof. Reduce $A_{TM}$ to $ALL_{PDA}$ by the computation history method.

$EQ_{CFG}$ is undecidable.

The Post Correspondence Problem (PCP) is undecidable. Proof. Reduce $A_{TM}$ to PCP by the computation history method.

$AMBIG_{CFG}$ is undecidable. Proof. PCP is mapping reducible to $AMBIG_{CFG}$.

The computation history method is useful for showing the undecidability of problems involving testing for the existence of some object. The object is the computation history in some form.

#### 2.3.2 Mapping reducibility

Function $f: \Sigma^{\ast} \to \Sigma^{\ast}$ is *computable* if there is a TM $F$ on input $w$ halts with $f(w)$ on its tape for all strings $w$. $A$ is *mapping-reducible* to $B$ ($A\le_{m} B$) if there is a computable function $f$ where $w\in A$ if and only if $f(w)\in B$.

If $A\le_m B$ then $\overline{A} \le_m \overline{B}$ by definition.

Example. $A_{TM} \le_m \overline{E_{TM}}$.

Theorem. Given $A\le_m B$. If $B$ is decidable/T-recognizable then $A$ is decidable/T-recognizable. If $A$ is undecidable/T-unrecognizable then $B$ is undecidable/T-unrecognizable. Proof. Immediate.

Usually, mapping reducibility is useful to prove T-unrecognizability: (template) give reduction function $f$. General reducibility (Turing reducibility) is useful to prove undecidability: (template) Assume TM $R$ decides $B$, then construct TM $S$ that decides $A$ (usually $A_{TM}$).

Caveat. $A$ is Turing reducible to $\overline{A}$, but $A_{TM}$ is T-recognizable while $\overline{A_{TM}}$ is not. Actually, $\overline{A_{TM}} \not\le_{m} A_{TM}$.

$E_{TM}$ is T-unrecognizable. Proof. $\overline{A_{TM}} \le_m E_{TM}$.

$EQ_{TM}$ and $\overline{EQ_{TM}}$ are T-unrecognizable. Proof. $\overline{A_{TM}} \le_m EQ_{TM}$ and $\overline{A_{TM}} \le_m \overline{EQ_{TM}}$.

### 2.4 Advanced topics in Computability Theory

#### 2.4.1 The recursion theorem

Theorem. There is a TM $SELF$ which on any input halts with $\langle SELF \rangle$ on the tape. Proof. $SELF$ has two parts, $A$ and $B$.

The recursion theorem. For any TM $T$ there is a TM $R$ that on all inputs $w$ operates in the same way as $T$ on input $\langle w, R \rangle$. Proof. $R$ has three parts: $A, B$ and $T$.

Moral. You can use "compute your own description" in describing TMs.

Example 1. A new proof for the undecidability of $A_{TM}$.

Example 2 (fixed point problem). For any computable function $f$, there is a TM $R$ such that $L(R) = L(S)$ where $f(\langle R \rangle) = \langle S \rangle$.

$M$ is a *minimal* TM if $|\langle M' \rangle| < |\langle M \rangle|$ implies $L(M') \neq L(M)$.

Example 3. $MIN_{TM}$ is T-unrecognizable. Proof. Assume some TM $E$ enumerates $MIN_{TM}$.

#### 2.4.2 Introduction to mathematical logic

## 3 Complexity Theory

Computability does not depend on computational models by Church-Turing Thesis. By contrast, complexity depends on models. However, the dependence is low (polynomial) for reasonable deterministic models.

### 3.1 Time complexity

#### 3.1.1 The Class P

TM $M$ *runs in time* $t(n)$ if $M$ always halts with $t(n)$ steps on all inputs of length $n$.

$TIME(t(n)) = \{B: \text{some deterministic 1-tape TM $M$ decides $B$ and $M$ runs in time $O(t(n))$} \}$.

Theorem. $A = \{a^kb^k: k\ge 0\} \in TIME(n \log n)$. Proof. Repeat crossing every other $a$ and $b$. Reject if even/odd parities disagree. Tight in light of the following theorem.

Theorem. If a language is decidable in $o(n \log n)$ time by a one-tape TM then it is regular.

Corollary. $TIME(n) =$ regular languages.

Theorem. Let $t(n) \ge n$. If a multi-tape TM decides $B$ in time $t(n)$, then $B\in TIME(t^2(n))$. Proof. In the conversion of multi-tape TM to one-tape TM, each step takes $O(t(n))$ steps in the one-tape TM.

All reasonable deterministic models are polynomially related, e.g., 1-tape TMs, multi-tape TMs, multi-dimensional TMs, random access machines, cellular automata.

Class $P := \bigcup_{k} TIME(n^k)$: polynomial-time decidable languages. $P$ is invariant for all reasonably deterministic models and corresponds roughly to realistically solvable problems.

$PATH = \{ \langle G, s, t \rangle: G$ is a directed graph with a path from $s$ to $t \}$.

Theorem. $PATH \in P$. Proof. Iteratively mark reachable nodes.

#### 3.1.2 The Class NP

An NTM *runs in time* $t(n)$ if all branches halt within $t(n)$ steps on all inputs of length $n$.

$NTIME(t(n)) = \{B: \text{some deterministic 1-tape NTM $M$ decides $B$ and $M$ runs in time $O(t(n))$} \}$.

Class $NP := \bigcup_k NTIME(n^k)$. $NP$ is invariant for all reasonable nondeterministic models and corresponds roughly to easily verifiable problems.

$HAMPATH := \{ \langle G, s, t \rangle: G$ is a directed graph with a path from $s$ to $t$ that goes through every node of $G \}$.

Theorem. $HAMPATH \in NP$. Proof. Nondeterministically guess a sequence of $m$ nodes (say $G$ has $m$ nodes).

$COMPOSITES = \{x: x$ is not prime and $x$ is written in binary$\}$.

Clearly, $COMPOSITES \in NP$. Theorem (2002). $COMPOSITES \in P$. 
Proof. Not covered. 

Corollary. $PRIME \in P$.

Theorem. $A_{CFG} \in NP$. Proof. Concert to Chomsky Normal Form. Try all derivations of length $2|w| - 1$.

Theorem. $A_{CFG} \in TIME(n^5) \subset P$. 
Proof. Dynamic programming: recursion + memory (the result of $\langle G, w, R \rangle$).

A Boolean formula $\phi$ is *satisfiable* if $\phi$ evaluates to be true for some assignment to its variables.

$SAT = \{\langle \phi \rangle: \phi$ is a satisfiable Boolean formula$\}$.

$A$ is polynomial-time reducible to $B$ ($A \le_P B$) if $A\le_m B$ by a reduction function that is computable in polynomial time.

**NP-completeness.**

A language $B$ is *NP-complete* if $B\in NP$ and for all $A\in NP$, $A\le_P B$.

Cook-Levin Theorem. $SAT$ is NP-complete. 
Proof. 1) $SAT \in NP$. 2) For $A\in NP$, let NTM $M$ decide it in $n^k$ time. Then construct $\phi_{M, w}$ to be satisfiable if and only if $M$ has an accepting computational history on $w$.

Theorem. $SAT\le_P 3SAT$. Proof. Use the tree structure of $\phi$ to add variables $z_1, z_2, \cdots$, and then construct a logically equivalent 3CNF.

Theorem. $If A \le_P B$ and $B\in P$ then $A\in P$. Proof. By definition.

A Boolean formula $\phi$ is in *Conjuctive Normal Form (CNF)* if it has the form Clause (Literal OR Literal OR\...) AND Clause AND\...

A 3CNF is a CNF with exactly 3 literals in each clause.

$3SAT = \{\langle \phi \rangle: \phi$ is a satisfiable 3CNF formula$\}$.

A *$k$-clique* in a graph is a subset of $k$ nodes all directly connected by edges.

$CLIQUE = \{ \langle G, k \rangle: \text{graph $G$ contains a $k$-clique} \}$.

Theorem. $3SAT\le_P CLIQUE$. Proof. Make each literal a node and add proper edges.

Theorem. $3SAT \le_P HAMPATH$. Proof. Use a zig-zag/zag-zig gadget to simulate a variable and a node to simulate a clause.

Theorem. $3SAT \le_P SUBSET-SUM$.

Theorem. $3SAT \le_P UHAMPATH$.

To show some language $C$ is NP-complete, we often show $3SAT \le_P C$ by constructing gadgets that simulate variables and clauses.

$coNP := \{\overline{A}: A\in NP\}$.

### 3.2 Space complexity

#### 3.2.1 PSPACE and NPSPACE

Let $f(n)\ge n$. A TM $M$ *runs in space* $f(n)$ if $N$ always halts and uses at most $f(n)$ *tape cells* on all inputs of length $n$. An NTM $M$ *runs in space* $f(n)$ if all branches halt and each branch uses at most $f(n)$ tape cells on all inputs of length $n$.

$SPACE(f(n)) := \{B: \text{some deterministic 1-tape TM $M$ decides $B$ and $M$ runs in space $O(f(n))$} \}$.

$NSPACE(f(n)) := \{B: \text{some 1-tape NTM $M$ decides $B$ and $M$ runs in space $O(f(n))$} \}$.

$PSPACE := \bigcup_{k} SPACE(n^k)$.

$NPSPACE := \bigcup_{k} NSPACE(n^k)$.

Theorem (Relationships between time and space complexity). $TIME(t(n)) \subset SPACE(t(n))$; $SPACE(t(n)) \subset TIME(2^{O(t(n))}) = \bigcup_{c} TIME (c^{t(n)})$.
Proof. The first is direct. For the second, A TM that uses more than $c^{t(n)}$ time with $t(n)$ tape cells must have repeated a configuration and looping for some $c$.

Corollary. $P \subset PSPACE$.

Theorem. $NP \subset PSPACE$. 
Proof. Direct, by using a TM to simulate the nondeterministic branches and reusing the space. An indirect way is to show $SAT \in PSPACE$ by trying all possible assignments and reusing the space.

Corollary. $coNP \subset PSPACE$. Proof. By noting $PSPACE$ is closed under complementation.

A *quantified Boolean formula (QBF)* is a Boolean formula with leading exists $\exists$ and for all $\forall$ quantifiers. All variables must lie within the scope of a quantifier.

A QBF is true or false.

$TQBF = \{\langle \phi \rangle: \phi$ is a QBF that is true$\}$.

Theorem. $TQBF \in SPACE(n) \subset PSPACE$. Proof. Evaluate a QBF by recursion on each variable.

#### 3.2.2 Savitch's theorem

A *ladder* is a sequence of strings of a common length where consecutive strings differ in a single symbol.

$LADDER_{DFA} = \{ \langle B, u, v \rangle: B$ is a DFA and $L(B)$ contains a ladder $y_1, \cdots, y_k$ (consecutive strings differ in a single symbol) where $y_1 = u$ and $y_k = v \}$.

Theorem. $LADDER_{DFA} \in NPSPACE(n)$. 
Proof. Nondeterministic guess the sequence from $u$ to $v$ by guessing one string at a time (cannot store sequence) and for at most $|\Sigma|^{|u|}$ steps (must terminate).

Theorem. $LADDER_{DFA} \in SPACE(n^2) \subset PSPACE$. 
Proof. Recursively solve $BOUNDED-LADDER_{DFA} = \{\langle B, u, v, b \rangle: \text{ladder of length} \le b\}$. Each recursive level uses $O(n)$ space and the recursion depth is $O(\log (|\Sigma|^{|u|})) = O(n)$.

Savitch's theorem. $NSPACE(f(n)) \subset SPACE(f^2(n))$. 
Proof. Convert an NTM to an equivalent TM by an argument similar to that for $LADDER_{DFA \in PSPACE}$ where each string is a configuration. *Modify the TM to erase work tape and move heads to left end upon accepting to have a single accepting configuration.* The construction requires knowing $f(n)$; to this end we can try $f(n) = 1, 2, \cdots$.

Corollary. $PSPACE = NPSPACE$.

#### 3.2.3 PSPACE-completeness

A language $B$ is *PSPACE-complete* if $B\in PSPACE$ and for all
$A\in PSPACE$, $A \le_P B$.

Theorem. $TQBF$ is PSPACE-complete. Proof. 1) We have shown
$TQBF \in PSPACE$. 2) For all $A\in PSPACE$, let $M$ decide it in $n^k$ space. On input $w$, construct a QBF of size $O(n^{2k})$ to be true if and only if $M$ has an accepting computational history on $w$. The proof works even if $M$ is an NTM, so provides an alternative proof for Savitch's theorem.

*The Generalized Geography Game*. Played on any directed graph. Players take turns picking nodes that form a simple path. The first player stuck loses.

$GG = \{\langle G, a \rangle$ Player I has a *forced win* (winning strategy if both players play optimally) in Generalized Geography on graph $G$ starting at node $a\}$. Note that in GG, one of the players has a forced win.

*The Formula Game*. Given QBF $\phi$, there are two Players $\exists$ and $\forall$. Player $\exists$ assigns values to the $\exists$-quantified variables. Player $\forall$ assigns values to the $\forall$-quantified variables. The players choose the values according to the order of the quantifiers in $\phi$ (not alternately). After all variables have been assigned values, we determine the winner: Player $\exists$ wins if the assignment satisfies $\phi$. Player $\forall$ wins if not.

Claim. Player $\exists$ has a forced win in the formula game on $\phi$ iff $\phi$ is true. Therefore, $\{\langle \phi \rangle:$ Player $\exists$ has a forced win on $\phi\} = TQBF$.

Theorem. $GG$ is PSPACE-complete. 
Proof. 1) $GG\in PSPACE$ recursively. 2) $TQBF\le_P GG$ by constructing a GG $G$ to mimic the formula game on $\phi$. Use a gadget to simulate a variable and another gadget to simulate a clause.

#### 3.2.4 Log space

To define sublinear space computation, do not count input as part of space used. Use 2-tape TM model with read-only input tape.

Define $L := SPACE(\log n)$, $NL := NSPACE(\log n)$. Log space can represent a constant number of pointers into the input.

Theorem. $\{ww^R: w\in \Sigma^{\ast}\}\in L$. Proof. Store points.

Theorem. $PATH \in NL$. Proof. Nondeterministically guess the path (store the current node).

Whether $L = NL$ is unsolved.

Theorem. $L \subset P$. 
Proof. Say $M$ decides $A\in L$ in log space. The total number of configuration is $O(n^k)$ for some $k$, so $M$ runs in polynomial time.

Theorem. $NL \subset SPACE(\log^2 n)$. 
Proof. Savitch's theorem works for log space.

Theorem. $NL \subset P$. 
Proof. Say NTM $M$ decides $A\in NL$ in log space. On input $w$, build a configuration graph $G_{M, w}$. Accept if and only if there is a path from $c_{start}$ to $c_{accept}$.

A *log-space transducer* is a TM with three tapes: 1) read-only input tape of size $n$, 2) read/write work tape of size $O(\log n)$, 3) write-only output tape.

A log-space transducer $T$ computes a function $f: \Sigma^{\ast} \to \Sigma^{\ast}$ if $T$ on input $w$ halts with $f(w)$ on its output tape for all $w$. Say that $f$ is *computable in log space*. $A$ is *log-space reducible* to $B$ ($A\le_L B$) if $A\le_m B$ by a reduction function that is computable in log space.

Note that all log-space reductions are polynomial-time reductions. The converse is not true.

$B$ is *NL-complete* if $B\in NL$ and for all $A\in NL$, $A\le_L B$.

Theorem. If $A\le_L B$ and $B\in L$ then $A\in L$. Proof. On input $w$, run decider for $B$ on $f(w)$. Since we don't have space to store $f(w)$, we recompute symbols of $f(w)$ as needed.

Theorem. $PATH$ is NL-complete. Proof. Give a log-space reduction $f(w) = \langle G, s, t \rangle$ such that $w\in A$ if and only if $G$ has a path from $s$ to $t$ by computational histories.

Theorem. $\overline{2SAT}$ is NL-complete. 
Proof. 1) $2SAT \in NL$ and by closure to complementation. 2) Show $PATH \le_L \overline{2SAT}$ by putting clause $x_u \to x_v$ for edge $(u, v) \in G$.

Theorem (Immerman-Szelepcsényi). $NL = coNL$. 
Proof. Show $\overline{PATH} \in NL$. 
Say *NTM $M$ computes function* $f: \Sigma^{\ast} \to \Sigma^{\ast}$ if for all $w$ 1) All branches of $M$ on $w$ either halt with $f(w)$ on the tape or reject. 2) Some branch of $M$ on $w$ does not reject. Claim that some NL machine (log-space NTM) computes $path_d$ (as a function that outputs YES or NO) if and only if some NL machine computes $c_d = c_d(G, s) = \#$ nodes reachable from $s$ via a path of length $\le d$ (key to the proof). Iteratively compute $c_{d+1}$ from $c_d$ until $d = \#$ nodes in $G$. Then compute function $path_m$.

### 3.3 Intractability

#### 3.3.1 Hierarchy theorems

Space hierarchy theorem. For space constructibile function
$f: \mathbb{N}\to \mathbb{N}$, there is a language $A$ which is
decidable in $O(f(n))$ space but not decidable in $o(f(n))$ space.
Proof. Diagonalization.

Note that $\log \log n$ is not space constructibile.

Time hierarchy theorem. For time constructibile function $f: \mathbb{N}\to \mathbb{N}$, there is a language $A$ which is decidable in $O(f(n))$ time but not decidable in $o(f(n)/\log(f(n)))$ time. Proof. Diagonalization. The log factor comes from a counter that counts the number of steps.

Corollary. $NL \subset SPACE(\log^2(n)) \subsetneq SPACE(n) \subset PSPACE$.

Corollary. $TQBF \notin NL$. Proof. The polynomial-time reduction for showing TQBF is PSPACE-complete can be done in log space.

$EXPTIME := \bigcup_{k} TIME(2^{n^k})$.
$EXPSPACE := \bigcup_{k} SPACE(2^{n^k})$.

$B$ is *EXPTIME-complete* if 1) $B\in EXPTIME$, 2) for all
$A \in EXPTIME$, $A \le_P B$. Same for *EXPSPACE-completeness*.

Theorem. If $B$ is EXPTIME-complete then $B\notin P$.

Theorem: If $B$ is EXPSPACE-complete then $B\notin PSPACE$.

$EQ_{REX} := \{\langle R_1, R_2 \rangle: R_1$ and $R_2$ are equivalent regular expressions$\}$.

Theorem: $EQ_{REX} \in PSPACE$. Proof: Show $\overline{EQ_{REX}} \in NPSPACE$.

Exponentiation: $R^k$ to mean $RR\cdots R$.

$EQ_{REX\uparrow} := \{\langle R_1, R_2 \rangle: R_1$ and $R_2$ are equivalent regular expressions with exponentiation$\}$.

Theorem (a provably intractable problem). $EQ_{REX\uparrow}$ is EXPSPACE-complete. 
Proof. 1) $EQ_{REX\uparrow} \in EXPSPACE$ by expanding exponentiation and $EQ_{REX} \in PSPACE$. 2) Say $M$ decides $A\in EXPSPACE$ in space $2^{n^k}$. Give a polynomial-time reduction $f: A\to EQ_{REX\uparrow}$. $f(w) = \langle R_1, R_2 \rangle$ where $R_2 = \Delta^{\ast}$ and $R_1$ accepts all strings except a rejecting computation history for $M$ on $w$: bad-start, or bad-move, or bad-reject.

#### 3.3.2 Oracles

Let $A$ be any language. A TM $M$ with oracle for $A$, written $M^A$, is a TM equipped with a black box that can answer queries "is $x\in A$?" for free.

$P^A := \{B: B$ is decidable in polynomial time with an oracle for $A\}$.

Example. $NP \in P^{SAT}$. $coNP \in P^{SAT}$. If $NP = P^{SAT}$ then $NP = coNP$.

$NP^A := \{B: B$ is decidable in nondeterministic polynomial time with an oracle for $A\}$.

$MIN-FORMULA = \{\langle \phi \rangle: \phi$ is a minimal Boolean formula $\}$.

Theorem. $\overline{MIN-FORMULA} \in NP^{SAT}$. Proof. Guess a shorter formula and use SAT oracle to solve the coNP problem $EQ_{FORMULA}$.

Theorem. There is an oracle $A$ such that $P^A = NP^A$. There is an oracle $B$ such that $P^B \neq NP^B$. Proof. Let $A = TQBF$.

Implication. The diagonalization method cannot be used to show $P \neq NP$, since the same argument would show $P^A \neq NP^A$ for any oracle $A$.

### 3.4 Advanced topics in Complexity Theory

#### 3.4.1 Probabilistic algorithms

A *probabilistic Turing machine (PTM)* is a variant of a NTM where each computation step has 1 or 2 possible choices.

$\mathbb{P}(\text{branch } b) = 2^{-k}$ where $b$ has $k$ coin flips. 
$\mathbb{P}(M \text{ accepts } w) = \sum_{b \text{ accepts}} \mathbb{P}(\text{branch } b)$.
$\mathbb{P}(M \text{ rejects } w) = 1 - \mathbb{P}(M \text{ accepts } w)$.

For $\epsilon \ge 0$, say *PTM $M$ decides language $A$ with error probability $\epsilon$* if for every $w$, the probability of giving the wrong answer about $w\in A$ is $\le \epsilon$.

$BPP := \{A:$ some polynomial-time PTM decides $A$ with error $\epsilon = 1/3\}$.

Amplification lemma. If $M$ is a poly-time PTM with error $\epsilon_1 \le 1/2$ then on input of length $n$ for any $0 < \epsilon < 2^{-poly(n)}$, there is an equivalent poly-time PTM $M$ with error $\epsilon_2$. Proof. Repeat and take the majority response.

Theorem. BPP is closed under union, complementation. $P \subset BPP \subset PSPACE$.

A *branching program (BP)* is a directed, acyclic graph that has 1) query nodes labeled $x_i$ and having two outgoing edges labeled $0$ and $1$, 2) two output nodes labeled 0 and 1 and having no outgoing edges, 3) a designated start node.

BP $B$ with query nodes $x_1, \cdots, x_m$ describes a Boolean function $f: \{0, 1\}^m \to \{0, 1\}$.

BPs are equivalent if they describe the same Boolean function.

$EQ_{BP} := \{ \langle B_1, B_2 \rangle: B_1$ and $B_2$ are equivalent BPs (written as $B_1 \equiv B_2$) $\}$.

Theorem. $EQ_{BP}$ is coNP-complete. Proof. Show that $\overline{EQ_{BP}}$ is NP-complete by reducing $3SAT$ to it.

If $EQ_{BP} \in BPP$ then $NP \subset BPP$. This would be surprising since we conceive BPP is close to P.

A BP is *read-once* if it never queries a variable more than once on any path from the start node to an output.

$EQ_{ROBP} := \langle B_1, B_2 \rangle: B_1$ and $B_2$ are equivalent read-once BPs $\}$.

Theorem. $EQ_{ROBP} \in BPP$. Proof. Arithmetization: convert the Boolean formula to a polynomial and run $B_1$ and $B_2$ on a non-Boolean input, drawn uniformly at random in the filed $\mathbb{F}_q$ for a prime $q\ge 3m$ where $m$ is the number of variables. We need the following lemmas.

Polynomial Lemma. If $p(x) \neq 0$ is polynomial of degree $\le d$ then $p$ has $\le d$ roots. This lemma holds for any field $\mathbb{F}$. Here we use a finite field $\mathbb{F}_q$ with $q$ elements where $q$ is prime and $+, \times$ operate $\bmod q$.

Corollary. If $p(x) \neq 0$ has degree $\le d$ and we pick a random $r\in \mathbb{F}_q$, then $\mathbb{P}(p(r) = 0) \le d/q$. Proof. There are at most $d$ roots out of $q$ possibilities.

Theorem (Schwartz-Zippel). If $p(x_1, \cdots, x_m)\neq 0$ has degree $\le d$ in each $x_i$ and we pick random $r_1, \cdots, r_m \in \mathbb{F}_q$ then $\mathbb{P}(p(r_1, \cdots, r_m) = 0) \le md/q$. Proof. By induction.

#### 3.4.2 Interactive proof systems

Undirected graphs $G$ and $H$ are *isomorphic* if they are identical except for a permutation (rearrangement) of the nodes.

$ISO = \{ \langle G, H \rangle: G$ and $H$ are isomorphic graphs $\}$. $ISO \in NP$ is obvious, but we do not know whether $ISO \in P, ISO$ is NP-complete, or $\overline{ISO} \in NP$.

In an *interative proof system*, there are two interacting parties: a verifier $V$ which is a probabilistic polynomial-time TM and a prover $P$ that has unlimited computational power. Both $P$ and $V$ see input $w$. They exchange a polynomial number of polynomial-size messages. Then $V$ accepts or rejects.

$IP := \{ A:$ for some $V$ and $P$ (This $P$ is an "honest" prover) $w\in A \Rightarrow \mathbb{P}((V\leftrightarrow P)$ accepts $w) \ge 2/3$; $w \notin A \Rightarrow$ for any prover $\tilde{P}$ ($\tilde{P}$ is a "crooked" prover trying to make V accept when it shouldn't) $\mathbb{P}((V \leftrightarrow P)$ accepts $w) \le 1/3 \}$. 
Note that an amplification lemma can improve the error probability from $1/3$ to $1/2^{poly(n)}$.

Theorem. $\overline{ISO} \in IP$. Proof. $V$ randomly send permuted $G$ or $H$ to $P$ and see if $P$ identifies the correct one. Repeat another time. Accept if $P$ is correct both times. Reject otherwise.

Theorem. $IP = PSPACE$. Proof. $IP \subset PSPACE$ obviously. The other direction is similar to the proof of $coNP \subset IP$ below.

$\#SAT := \{ \langle \phi. k \rangle:$ Boolean formula $\phi$ has $k$ satisfying assignments $\}$.

Language $B$ is *NP-hard* if $A \le_P B$ for every $A \in NP$.

Theorem. $\#SAT$ is coNP-hard. Proof. Show $\overline{SAT} \le_P \#SAT$ by $f(\langle \phi \rangle) = \langle \phi, 0 \rangle$.

Theorem. $coNP \subset IP$. 
Proof. Show $\#SAT \in IP$. Let $\phi$ has variables $x_1, \cdots, x_m$. Let $\phi(a_1\cdots a_i)$ be $\phi$ with $(x_1, \cdots, x_i) = (a_1, \cdots, a_i)$. Call $a_1, \cdots, a_i$ *presets*. The remaining variables stay unset. Let $\#\phi(a_1\cdots a_i)$ be the number of satisfying assignments of $\phi(a_1\cdots a_i)$. We claim that $\#\phi(a_1\cdots a_i) = \sum_{a_{i+1}, \cdots, a_m \in \{0, 1\}} \phi(a_1, \cdots, a_m)$. The rest goes by arithmetization. The resulting polynomial $\phi$ has a degree of at most $|\phi|$.
