---
bibliography: modules/bibliography.bib
author:
- name: Michal Gregor
  affiliation: '<span class="en">
                <div>Department of Control</div>
                <div style="margin-bottom:15px">and Information Systems</div>
                <div>
                    University of Žilina
                </div>
                </span>
                <span class="sk">
                <div>Katedra riadiacich</div>
                <div style="margin-bottom:15px">a informačných systémov</div>
                <div>
                    Žilinská univerzita
                </div>
                </span>'
  email: michal.gregor@uniza.sk
title: '<span class="en">L2: Object Detection</span>
        <span class="sk">L2: Detekcia objektov</span>'
subtitle: '<span class="en">Computer Vision</span>
           <span class="sk">Počítačové videnie</span>'
#date: 24. 3. 2020
intro-left: '<p style="margin-top: 50px;">
             <img src="modules/feit_logo.svg" class="inline-img" style="height:100px" />
             <span class="en"><img src="modules/luiza_logo_full_en.svg" class="inline-img" style="height:85px" /></span>
             <span class="sk"><img src="modules/luiza_logo_full.svg" class="inline-img" style="height:85px" /></span>
             </p>'
slideNumber: c/t
customtheme: reveal/uniza_theme/luiza.css
intro-right: "<img src=\"modules/luiza_intro.png\" style=\"height: 400px; margin-top: 30px; margin-bottom: 70px;\">"
langs: "en:English,sk:Slovenčina"
---

# [Computer Vision Tasks]{.en} [Úlohy počítačového videnia]{.sk}

![](images/computer_vision/tasks/cv_tasks.svg){width="80%"}

:::{onslide="2-" .space-before15 .centering}
[**So how do we represent object detection using a neural net?**]{.en}
[]{.sk}
:::

## Fluchta

6789

## [Classification]{.en} [Klasifikácia]{.sk}
[{{heading1}}]{.subtitle}

* [We already know how to do classification so let's start with that;]{.en}
  []{.sk}

  * [**Fixed size input:** we resize our image to some fixed size;]{.en}
    []{.sk}
  
  * [**Feature extraction:** we use a bunch of convolutional layers to **extract features**;]{.en}
    []{.sk}
    {onslide="2-"}

  * [**Classification:** we add one/several **fully-connected** layers to do the **classification**;]{.en}
    []{.sk}
    {onslide="3-"}

:::{.space-before15 .space-after1}
![](images/computer_vision/task_repre/classification_1.svg){width="75%" only="1"}
![](images/computer_vision/task_repre/classification_2.svg){width="75%" only="2"}
![](images/computer_vision/task_repre/classification.svg){width="75%" only="3-"}
:::

* [**Network's outputs:**]{.en}
  []{.sk}
  {onslide="4-"}

  * [As many logits as there are classes;]{.en}
    []{.sk}
  
  * [Logits passed through softmax to get probabilities;]{.en}
    []{.sk}
  
  * [Minimize the cross-entropy loss;]{.en}
    []{.sk}

  * [We predict the most probable class;]{.en}
    []{.sk}

## [Localization]{.en} [Lokalizácia]{.sk}
[{{heading1}}]{.subtitle}

:::{.spread05 .space-before05}
* [Localization is easy to represent;]{.en}
  []{.sk}

* [Just add another top: a **bounding box regressor**;]{.en}
  []{.sk}

  * [Predicts bounding box corners $(x_1, y_1)$, $(x_2, y_2)$;]{.en}
    []{.sk}

  * [Regression, i.e. use the MSE loss;]{.en}
    []{.sk}
:::

![](images/computer_vision/task_repre/localization.svg){width="75%" .negspace-before15}

## [Object Detection]{.en} [Detekcia objektov]{.sk}
[{{heading1}}]{.subtitle}






# Mean Average Precision (mAP) {.empty}

:::::{.columns}
:::::{.column width="15%"}
:::::
:::::{.column width="70%" .spread1}

* [Object detectors are typically evaluated in terms of **mean Average Precision (mAP)**;]{.en}
  []{.sk}

* [We need to explain a couple of concepts before mAP;]{.en}
  []{.sk}
  {onslide="2-"}

  * [**Intersection over union (IoU):** a way to match bounding boxes;]{.en}
    []{.sk}

  * [**The precision-recall curve:** how precision changes with recall;]{.en}
    []{.sk}

  * [**Average precision:** area under the precision-recall curve;]{.en}
    []{.sk}

:::::
:::::{.column width="15%"}
:::::
:::::

## Intersection over Union (IoU)
[{{heading1}}]{.subtitle}

:::::{.columns .space-before05}
:::::{.column width="49%"}

:::{.space-before1 .spread15}
* [How do we tell whether two bounding boxes match?]{.en}
  [Ako určíme, či sa dva ohraničujúce rámce zhodujú?]{.sk}
  
  * [We need some measure of how much they overlap...]{.en}
    []{.sk}
    {.space-before05}

* [**Intersection over union**;]{.en}
  [**Prienik nad zjednotením**;]{.sk}
  {onslide="2-"}

  :::{.space-before05 .spread05}
  * [A measure of how much overlap there is;]{.en}
    []{.sk}

  * [If **IoU is $\geq$ threshold**, there is a match;]{.en}
    []{.sk}

  * [Otherwise there is not;]{.en}
    []{.sk}
  :::

* [Object detectors are often evaluated at a range of different IoU thresholds;]{.en}
  []{.sk}
  {onslide="3-"}

  * [More on this later;]{.en}
    []{.sk}
:::

:::::
:::::{.column width="2%"}
:::::
:::::{.column width="49%" onslide="2-"}
![](images/computer_vision/iou.svg){width="100%"}
<!-- ![](images/computer_vision/iou_0.svg){width="80%"} -->
:::::
:::::

## [Recap: Precision and Recall]{.en} [Opakovanie: presnosť a úplnosť]{.sk}
[{{heading1}}]{.subtitle}

* [Recall the **confusion matrix** for a binary classification problem:]{.en}
  []{.sk}

::::{style="font-size: 90%" .space-after05}
::::{.en}
<table class="borderless">
<tr>
    <td></td>
    <td></td>
    <td colspan="2" class="centering"><b>actual class</b></td>
</tr>
<tr>
    <td></td>
    <td></td>
    <td class="centering"><b>pos.</b></td>
    <td class="centering"><b>neg.</b></td>
</tr>
<tr>
    <td rowspan="2" class="vcentering"><b>predicted class</b></td>
    <td><b>pos.</b></td>
    <td style="border-top: 1px solid; border-left: 1px solid;">
        true positive (TP) <br />
        <em>correct</em>
    </td>
    <td style="border-top: 1px solid; border-left: 1px solid; border-right: 1px solid;">
        false positive (FP) <br />
        <em>type I error</em>
    </td>
</tr>
<tr>
    <td><b>neg.</b></td>
    <td style="border-top: 1px solid; border-left: 1px solid; border-bottom: 1px solid; ">
        false negative (FN) <br />
        <em>type II error</em>
    </td>
    <td style="border-top: 1px solid; border-left: 1px solid; border-bottom: 1px solid; border-right: 1px solid;">
        true negative (TN) <br />
        <em>correct</em>
    </td>
</tr>
<tr>
    <td></td>
    <td><b>sums:</b></td>
    <td class="centering">P</td>
    <td class="centering">N</td>
</tr>
</table>
::::

::::{.sk}
<table class="borderless">
<tr>
    <td></td>
    <td></td>
    <td colspan="2" class="centering"><b>reálna trieda</b></td>
</tr>
<tr>
    <td></td>
    <td></td>
    <td class="centering"><b>poz.</b></td>
    <td class="centering"><b>neg.</b></td>
</tr>
<tr>
    <td rowspan="2" class="vcentering"><b>predikovaná trieda</b></td>
    <td><b>poz.</b></td>
    <td style="border-top: 1px solid; border-left: 1px solid;">
        skutočne pozitívne (TP) <br />
        <em>korektný výstup</em>
    </td>
    <td style="border-top: 1px solid; border-left: 1px solid; border-right: 1px solid;">
        falošne pozitívne (FP) <br />
        <em>chyba I. typu</em>
    </td>
</tr>
<tr>
    <td><b>neg.</b></td>
    <td style="border-top: 1px solid; border-left: 1px solid; border-bottom: 1px solid; ">
        falošne negatívne (FN) <br />
        <em>chyba II. typu</em>
    </td>
    <td style="border-top: 1px solid; border-left: 1px solid; border-bottom: 1px solid; border-right: 1px solid;">
        skutočne negatívne (TN) <br />
        <em>korektný výstup</em>
    </td>
</tr>
<tr>
    <td></td>
    <td><b>súčty:</b></td>
    <td class="centering">P</td>
    <td class="centering">N</td>
</tr>
</table>
::::
::::

:::::{.columns}
:::::{.column width="49%" onslide="2-"}

[Precision]{.block .en}
[Presnosť]{.block .sk}

* [How often we are right when predicting the positive class:]{.en}
  [Ako často máme pravdu keď predikujeme pozitívnu triedu:]{.sk}

  :::{.space-before15}
  [$$
  \text{precision} = \frac{\text{TP}}{\text{TP} + \text{FP}}
  $$]{.en}
  [$$
  \text{presnosť} = \frac{\text{TP}}{\text{TP} + \text{FP}}
  $$]{.sk}
  :::

:::::
:::::{.column width="2%"}
:::::
:::::{.column width="49%" onslide="3-"}

[Recall]{.block .en}
[Úplnosť]{.block .sk}

* [Proportion of really positive samples that we managed to catch:]{.en}
  [Podiel reálne pozitívnych vzoriek, ktoré sa podarilo zachytiť:]{.sk}
  
  :::{.space-before15}
  [$$
  \text{recall} = \frac{\text{TP}}{\text{P}} = \frac{\text{TP}}{\text{TP} + \text{FN}}
  $$]{.en}
  [$$
  \text{úplnosť} = \frac{\text{TP}}{\text{P}} = \frac{\text{TP}}{\text{TP} + \text{FN}}
  $$]{.sk}
  :::

:::::
:::::

## [The Precision-Recall Curve]{.en} [Krivka presnosti a úplnosti]{.sk}
[{{heading1}}]{.subtitle}

* [Displays **how precision changes with recall**;]{.en}
  []{.sk}
  {.space-before05}

:::::{.columns .space-before05}
:::::{.column width="60%"}
![](images/computer_vision/precision_recall_curve.svg){width="100%"}
:::::
:::::{.column width="40%"}

:::::
:::::












## Average Precision
[{{heading1}}]{.subtitle}















:::{only="1"}
``` {.include}
images/computer_vision/ap_example/AP_table1.html
```
:::
:::{only="2"}
``` {.include}
images/computer_vision/ap_example/AP_table2.html
```
:::








``` {.include}
modules/thankspage.md
```

## [References]{.en} [Zdroje]{.sk}

<div id="refs"></div>
