---
title: Tests classiques
author: Robin 'Pachichi' Boucher
tags: ING2, cours, maths
---

# Tests classiques

## Rappels de la loi gamma et loi normale

### Loi gamma $\gamma_r$
++Déf:++
Soit X une variable aléatoire continue positive. On dit que X suit la loi $\gamma_r$ (de paramètre $r > 0$) si sa densité est $f(x) = \frac{1}{\Gamma(r)}e^{-x}.x^{r-1}$, $\forall x > 0$ où $\Gamma(x) = \int_0^{+\infty}e^{-t}t^{x-1}dt$ est la fonction gamma.

++Propriétés de $\Gamma(x)$:++
(1) $\Gamma(x+1) = x\Gamma(x)$ ~~un truc~~
(2) $\Gamma(1) = 1$
(3) $\Gamma(n+1) = n!$
(4) $\Gamma(k \ast \frac{1}{2}) = \frac{(1.3.5...2k-1)}{2^k}\Gamma(\frac{1}{2})$
(5) $\Gamma(\frac{1}{2}) = \sqrt{\pi}$

++Calcul de $E(X)$ et de $V(X)$:++

$E(X) = \frac{1}{\Gamma_r} \int_0^{+\infty} x^re^{-x}dx = \frac{\Gamma(r+1)}{\Gamma(r)} = r$
$(E(x) = \int_0^{+\infty} xf(x)dx)$
$E(X^2) = \int_0^{+\infty} x^2f(x)dx = \frac{1}{\Gamma(r)} \int_0^{+\infty} x^{r+2}e^{-x}dx$
$E(X^2) = \frac{\Gamma(r+2)}{\Gamma(r)} = \frac{(r+1) \Gamma(r+1)}{\Gamma(r)} = (r+1)r$

Donc $V(X) = E(X^2) - E^2(X) = r(r+1) - r^2 = r$

### Loi Laplece-Gauss (loi normale)
++Déf:++
X suit la loi normale $N(m, \sigma)$ de paramètres $m$ et $\sigma$ si sa densité est $f(x) = \frac{1}{\sigma\sqrt{2\pi}} . e^{(-\frac{1}{2} . (\frac{x-m}{\sigma})^2 )}$, $\forall x \in \mathbb{R}$ avec
- $m = E(X)$
- $\sigma = \sqrt{V(X)}$

## Variable normale centrée et réduite
Soit X tend vers $N(m, \sigma)$
On pose $U = \frac{X - m}{\sigma}$, variable normale centrée et réduite.
Sa densité est :
> $f(u) = \frac{1}{\sqrt{2\pi}} e^{-\frac{U^2}{2}}$

$E(U) = \frac{E(X) - m}{\sigma} = 0$
$U$ est centrée.

Montrons que $V(U) = 1$
$V(U) = E(U^2) - E^2(U) = E(U^2)$
$V(U) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{+\infty} u^2 e^{-\frac{u^2}{2}}du = \frac{2}{\sqrt{2\pi}} \int_0^{+\infty} u^2 e^{-\frac{u^2}{2}}du$

Posons $t = \frac{u^2}{2} \Rightarrow dt = u du =\Rightarrow du = \frac{dt}{u} \Rightarrow du = \frac{dt}{\sqrt{2t}}$

$V(U) = \frac{2}{\sqrt{2\pi}} \int_0^{+\infty} 2t e^{-t} \frac{dt}{\sqrt{2t}} = \frac{2}{\sqrt\pi} \int_0^{+\infty} t^{\frac{1}{2}} e^{-t} dt$

$V(U) = \frac{2}{\sqrt\pi} \int_0^{+\infty} t^{\frac{1}{2}} e^{-t} dt = \frac{2}{\sqrt\pi} \Gamma(\frac{3}{2})$
$V(U) = \frac{2}{\sqrt\pi} \frac{1}{2} \Gamma(\frac{1}{2}) = \frac{\sqrt\pi}{\sqrt\pi} = 1$

> $V(U) = 1$

$U$ tend vers $N(0, 1)$

### Calculs des moments de la loi $N(0, 1)$
Soit $U$ une variable aléatoire de loi $N(0, 1)$

++Déf:++
On appelle moment d'ordre $k$ de $U$:
$m_k = E(U^k) = \int_\mathbb{R} U^k \frac{1}{\sqrt{2\pi}} e^{-\frac{U^2}{2}} du$
si $k$ est impair: $k = 2p+1$, $m_{2p+1} = \int_\mathbb{R} U^{2p+1} \frac{1}{\sqrt{2\pi}} e^{-\frac{U^2}{2}} du = 0$ avec $U^{2p+1} \frac{1}{\sqrt{2\pi}} e^{-\frac{U^2}{2}}$ **impair**
si $k$ est pair: $k = 2p$



# Rappels généraux
**La densité d'une variable aléatoire:** Fonction positive, dont l'intégrale sur l'espace vaut 1

Pour une **fonction impaire**: $\int_{-n}^nf(x)dx = 0$

Pour une **fonction paire**: $\int_{-n}^nf(x)dx = 2\ast \int_0^n f(x)dx$

Pour pouvoir utiliser la table, il faut toujours utiliser la ~~quoi~~ réduite.

Soit Fourrier discret si variable discrète, soit Fourrier continu si variable continue.

La loi binomiale $B(n, p)$ c'est une somme de variables de Bernouilli indépendantes.

Méthodes de Newton ou passer par l'indépendance.

Pour la loi de Poisson: $P(X=k) = e^{-\lambda}.\frac{\lambda^k}{k!}$

# Misc
Mac-laurin