# Defences against label poisoning
An illustration of 2 basic defences against gathering inaccurately labelled data.

## Intro

1. For many problems, we must gather data
2. Gathered data may be inaccurate, possibly maliciously so
3. Thus we should implement techniques to defend against inaccurare training data damaging our models.
4. Here I present 2 basic but surprisingly effective techniques for checking whether labels are accurate.

## Results

They may not be visible in the `.ipynb` so I've stuck them here aswell.

For each dataset we are testing: 
1. Given all examples with accurate labels how many does the check incorrectly dicsraded?
2. Given all examples with inaccurate labels how many does the check incorrectly accept?

We want to minimise both these values.

### Checking by difference

<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-difference/accurate-examples-discarded.png">
<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-difference/inaccurate-examples-accepted.png">
<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-difference/crossing-points.png">

### Checking by committee

<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-committee/accurate-examples-discarded.png">
<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-committee/inaccurate-examples-accepted.png">
<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-committee/combined.png">
<img height="200" src="https://github.com/JonathanWoollett-Light/defences-against-label-poisoning/blob/main/results/checking-by-committee/min-points.png">
