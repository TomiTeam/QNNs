# QNNs

This is a repository for my experiments on Quantum Neural Networks and Quantum Machine Learning via Cirq and TensorFlow
Quantum

The most prominent project is QTx, a failed (by the moment) model for stochastic completion of sentences
(it's also the only part of the code that it's fully documented at the moment).

QTx:
------------------------------

### Explanation of concept:

It's works on the basis that phrases in language work on a stochastic manner: if you're listening to someone that says "
my name is..." probably the next word is a proper noun. If you are task to guess the next word like on the board
game [Guess Who?](https://www.google.com/search?q=guess+who%3F&safe=active&rlz=1C1GCEA_enES784ES784&sxsrf=ALeKk024lTX8CsWgIWM7h_he7S16VDHwJw:1608242537721&source=lnms&tbm=isch&sa=X&ved=2ahUKEwjOnLGpgtbtAhVExYUKHQc-C9IQ_AUoAXoECCEQAw&biw=958&bih=920)
, and if you got for example some verbs on the table you probably would toss them out.

Now that we got how a stochastic way of thinking about language, although it is not very powerful, we can implement it
through
[quantum circuits](https://en.wikipedia.org/wiki/Quantum_circuit) (QCs) that behave stochastically by their own nature.
QCs consist of a series of quantum gates that are applied on a specific order, like the words on sentences.  
If we create QCs that are equivalent to sentences with the words as a quantum gates (with all the words except the last
one), we could in theory optimize them in such a way that upon measuring we get a bitstring equivalent to the last word
of the sentence the circuit will have learned how to complete sentences.

Here you have a QC diagram to ilustrate the idea:
![Hello my name is...](https://media.discordapp.net/attachments/549524193906130944/789925326369062942/unknown.png?width=1055&height=504)
In this case the measurement of the qubits has to be a proper noun for the sentence to make sense.

But the actual quantum circuit would this one:
![Rx..](https://cdn.discordapp.com/attachments/549524193906130944/789926095642165268/unknown.png)
With parameterized X gates applied to all the qubits, each word has it's own parameter (e.g. Theta1 is the parameter for
the gate equivalent to the word "Hello")

### Results:

As I already said, QTx is a failure:  
First I haven't even complete a full optimization, it just takes to long. Because the circuits are simulated on the Cirq
Simulator (Python), to solve this we need to decrease the complexity of the circuits (fewer qubits or fewer gates)
or simulate the circuits on a more efficient simulator (like [qsim](https://github.com/quantumlib/qsim) built on C++).  
The second thing is that is an inefficient model overall, I have that feeling, and you probably have it too. There isn't
a proper use of quantum superposition or entanglement on this model, the two powerful advantages of quantum computing. I
also think that is too simple to be efficient, we need something more complicated to get some good results, like a
sentence o word embedding based on superposition and entanglement for example