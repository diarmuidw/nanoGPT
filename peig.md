

# PeigGPT

This is a fork of the [nanoGPT](https://github.com/karpathy/nanoGPT), the simple but quick generative text repo. Thanks to Andrej for his super work and generosity.

I've included the text of Peig (technically "An old womans reflections") in english. 

Here's an example of the outoput 
```
The wind is the canoes of the sea us with Yellow Island. And may God grant us his soul! When I came to the eternal rest! When the Island to their souls! The one who are gone to the mackerel about Dingle
```

I've also incuded the text of Nimah by Peter O'leary as gaelge to see how the gerative text would handle the change of language, alphabet and grammar. 

[Niamh](https://www.gutenberg.org/ebooks/50913)

To run this you will need a GPU enabled workspace. I've used [Paperspace](http://www.paperspace.com) .

The first task is to tokenise the text. As each file is less that 1MB , there are limited tokens so this tokenises per character. This will mean that the generative text will be less accurate but for an experiment, it's still interesting.

```
python data/peig/prepare.py 
```

Next train. I've used pretty straightforward variable values here and not deep training to keep the time taken to be under an hour.  The droupout variable at 20% made a significant difference. 

```
python train.py config/train_peig.py --device=cuda --compile=False --eval_iters=20 --log_interval=1 --block_size=64 --batch_size=12 --n_layer=4 --n_head=4 --n_embd=128 --max_iters=1000 --lr_decay_iters=1000 --dropout=0.2
```

Next sample using a seed phrase. The system will carry on generating charater by charater to create some form of Peig-like prose! Not bad for a model based purely on one text.  I like "The wind that was not right that hurry on again than us is around them". I think if you said a few of these to a random Irish person they would say it could be Peig. I use a loop on a range of temperatures to generate with more or less variability. 

```
python sample.py --out_dir=out-peig  --start="The wind"
```

```
temp: 0.5
The wind that was drowned for the boat that was swallowed to the night. 'The night who'd be telling the night before the night that night \vith her. The poor girl was there before him. She had no wonder, but she didn't know
---------------
temp: 0.6
The wind is true for the carpenter's house. Kathleen's house I was hard then 'It was the people of the house,' said she. 'It was there before me,' said Sean, 'because she will to be in my life and Nell
---------------
temp: 0.7
The wind is the canoes of the sea us with Yellow Island. And may God grant us his soul! When I came to the eternal rest! When the Island to their souls! The one who are gone to the mackerel about Dingle, the
---------------
temp: 1
The wind of the canoes being drawn into the fields of Dunquin' Buoyant and everyone was no prospect could be some aid to the whitelections three white slender husband before us. They had nothing for the boys and they were written down as they were
---------------
temp: 1.1
The wind that was not right that hurry on again than us is around them. 'I have just on the same driving Heaven. I will be west only because myself here,' said her when Kate to ye are before that time. 'If you can, you
---------------
temp: 1.2
The wind wasn't calm for the night leaves catch me already. But the stalks, the water wasn't long until the lovely hollow 17 to go from the fence and called us across the potatoes went to our estate she couldn't have to go: , "
---------------
temp: 1.3
The wind that time is no purpose or thin, persuriment in his patience. This is a widow's desire for himself and strong and no amusement manner quiet only they'd see a fine and it were a spring story-field. A son of this 8
---------------
temp: 1.4
The wind is leaving them work!' Everyone was busy then. He took time being ready when \vas clean over these sons. It was closely standing on her towards the turf than home, and everyone spread into our parish boats backwards, beside her looking for the snail
---------------
temp: 1.5
The wind was looking their life looking by me on life. He spent that and land shining down on water. More and head came to a chair we'd ever packing into us lands.' 'Do for one,' said Kate, 'as all near a an elderly
```

The output of the Niamh book is as follows

```
python sample.py --out_dir=out-niamh --start="Tá mé"  #Tá mé means I am
```

```
temp: 0.5
Tá méid sin, agus níor bh’ fhada go mbeidh an uair sin, ach níor bh’fhada go raibh aon rud a dhéanamh
---------------
temp: 0.6
Tá méidh a dhéanamh d’á chéile.”“Ní fhéadfaidís an chailís ó shin a bhí agus í dh’fhá
---------------
temp: 0.7
Tá méid agus a chur chun an ngníomh san do ghluais agusadh an gcuma ’n-a raibh sé ’n-a bhfuil fhearraige
---------------
temp: 1
Tá méid sin, sar ar fhearaibh an taca so. An bhFiachrbat úd an Árdrígh do rug Murchadh. Bhí an chuid de mhór-sh
---------------
temp: 1.1
Tá mé ar uasa. Ní baoghal is leat, a tháinig sa cheart dó, mar a thug áthas dhuit le cuth go léir léir,[157] ‘agus
---------------
temp: 1.2
Tá méid sin leis an socair ’ná marbhughadh ag teacht thall ar Aifrinn.[272] ’ná chuigearna Easboig i gcóir agus na poibil
---------------
temp: 1.3
Tá mé a bheith ana Creide, aigeairtarach, cuimhneamh ab fághailtigh, í, sgéal ar dhul abhaile leis an ár n-
---------------
temp: 1.4
Tá méadaim sí ró maith mb’ iongnadh.“Chathail an Pháncuma san, a Thighearna Easboig,” arsa Niamh, “tá dro
---------------
temp: 1.5
Tá mé eile b’ siúbhal tagaithe air, tuitim áir nár fhéadfainn sar árd sór deas a dh’fhroch san anama
```
