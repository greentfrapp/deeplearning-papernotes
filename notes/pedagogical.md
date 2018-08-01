# [Interpretable and Pedagogical Examples](https://arxiv.org/abs/1711.00694)

### Smitha Milli, Pieter Abbeel, Igor Mordatch

#### 14 Feb 2018

---

### Concept

This is a paper on interpretability of models. Specifically, the paper considers the interpretability of *student-teacher networks*. The tasks considered typically show a concept that must be communicated from the teacher to the student, via examples of the concept selected by the teacher network, where both are neural networks.

A simple example from the paper is a task where the teacher has to convey the concept of a specific rectangle. To do so, the teacher can select points from the 2D space. The student will have to predict the coordinates of this specific rectangle based on the points given by the teacher. 

Given such a task, humans are likely to select points from inside the rectangle, in order to convey the concept of the rectangle's size and position. Under the constraint of minimal points selected, humans are likely to select points that represent opposing corners of the rectangle.

However, given the above task, teacher-student networks that are trained jointly tend to develop a language that is nonintuitive and difficult to interprete. For example, the teacher might select seemingly arbitrary points that have no relation to the given rectangle, but the student is still able to predict the correct rectangle. In that sense, the developed *language* has meaning to the teacher-student networks but are difficult to interpret for a human.

An example of a possible language that might develop but is difficult to interpret: the points given might be sampled from a distribution of vector sums over possible vectors that lie within the rectangle. Knowing the underlying logic, it might be possible to understand the language. It might be possible for the networks to arrive at such languages since there is no strong prior imposed on the possible languages. However, as humans, we tend to find simpler solutions that we denote as more *intuitive*. 

The paper then introduces what the authors term as 'Best Response' optimization. In essence, the student is first trained to predict concepts given random examples. The teacher is then trained to select the examples for the students. The two optimization stages occur one after another and only one at a time (ie. the student's weights are frozen during the teacher's training phase). The authors find that teacher-student networks trained in this manner show much more intuitive behavior, such as picking out corners of the rectangle in the above task.

In some sense, the BR optimzation process can be interpreted as imposing a strong prior on the possible languages that can be evolved during the teaching phase. When the teacher is being trained, the student is already conditioned on possible examples, which acts like a form of grounding. Specifically, using the rectangle example, during the student's training, the student never sees any points that are out of the rectangle. Then during the teacher's training, the teacher is forced to select the best points from inside the rectangle.
