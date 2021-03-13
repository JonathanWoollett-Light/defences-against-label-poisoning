# Defences against label poisoning 🛡️☣️

So I did this as a part of a university courework, [here is my report that went with the coursework](https://docs.google.com/document/d/1xGeCsTluex3-LeXJUQFmcZaMPhFfNahzu_bGJQOA2bs/edit?usp=sharing) if you care to read my frankly subpar writing (although it explains everything a bit more explicitly).

An illustration of 2 basic defences against gathering inaccurately labelled data.

## Intro

1. For many problems, we must gather data
2. Gathered data may be inaccurate, possibly maliciously so
3. Thus we should implement techniques to defend against inaccurate training data damaging our models.
4. Here I present 2 basic but surprisingly effective techniques for checking whether labels are accurate.



For each dataset we are testing: 
1. Given all examples with accurate labels how many does the check incorrectly discard?
2. Given all examples with inaccurate labels how many does the check incorrectly accept?

We want to minimise both these values.

## Defences

The graphs may not be visible in the `.ipynb` so I've stuck them here aswell.

```
this is some pseudo-code
```
```
Float D = max difference 
Float d = current difference
Uint S = samples
Uint s = current sample
```
### Checking by difference
```
[Float] p = example prediction
[Float] a_right = correct class average outputs
[Float] a_wrong = incorrect class average outputs
d_curve(0) = 0, d_curve(s) = d, d_curve(S) = 1
```
```
For each dataset:
    Predict all examples
    Average outputs for each class of examples
For s in range(S):
    d = d_curve(s)
    For each dataset:
        incorrectly_discarded = 0, incorrectly_accepted = 0
        For each example:
            If (abs(p - a_right) > d) then { incorrectly_discarded += 1 }
            Else if (abs(p - a_wrong) <= d) then { incorrectly_accepted += 1 }
        Store incorrectly_discarded and incorrectly_accepted  for this d and dataset combination

```

<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-difference/accurate-examples-discarded.png">
<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-difference/inaccurate-examples-accepted.png">
<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-difference/crossing-points.png">

### Checking by committee
```
Uint C = max committee size
Uint c = current committee size
Uint v = required votes
Uint d = predicted class label
Uint a_right = correct class label
Uint a_wrong = incorrect class label
```
```
For c in range(C): For each dataset: For _ in range(c):
    Fit c networks to training data
    Get each networks, class label predictions of test data
    Store networks and predictions
    For v in range(c):
        incorrectly_discarded = 0, incorrectly_accepted = 0
        For each example:
            correct = 0, wrong = 0
            For each network:
                If  (d = a_right) then { correct += 1 }
                Else if  ( d = a_wrong) then { wrong += 1 }
            If (correct < v) then { incorrectly_discarded += 1 }
            If (wrong >= v) then { incorrectly_accepted += 1 }
        Store incorrectly_accepted and incorrectly_accepted for this v, c and dataset combination.

```

<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-committee/accurate-examples-discarded.png">
<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-committee/inaccurate-examples-accepted.png">
<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-committee/combined.png">
<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-committee/min-points.png">
