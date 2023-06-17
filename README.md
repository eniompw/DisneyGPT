# DisneyGPT

* [Based on eniompw/nanoGPTshakespeare](https://github.com/eniompw/nanoGPTshakespeare)
* [Based on karpathy/nanoGPT](https://github.com/karpathy/nanoGPT)


### Train GPT
From Chars Tokens
* `# Get GrimmsFairyTales Dataset`  
`!cp ./nanoGPT/data/shakespeare_char/ ./nanoGPT/data/disney/ -r`   
`!sed -i "15s,.*,    data_url = 'https://raw.githubusercontent.com/eniompw/DisneyGPT/main/GrimmsFairyTales.txt'," ./nanoGPT/data/disney/prepare.py`

* `# Train nanoGPT on Dataset`  
`!cd ./nanoGPT && python train.py --dataset=DisneyChars --batch_size=12 --init_from='resume' --always_save_checkpoint=True --eval_interval=100 --max_iters=100`

From GPT2 Tokens
* `!cd ./nanoGPT && python train.py config/train_shakespeare_char.py --out_dir='out' --dataset=DisneyGPT --batch_size=12 --init_from='gpt2' --eval_interval=20 --max_iters=20`

### Run GPT

`!cd ./nanoGPT && python sample.py --num_samples=5 --max_new_tokens=20`

### Flags
`train.py` arguments explained:

* save model every 100 iters:
  * `--eval_interval=100`
* stop training after 300 iters:
  * `--max_iters=300`

* `init_from = 'resume' # 'scratch' or 'resume' or 'gpt2*'`
* `lr_decay_iters=2000 --max_iters=2000 # causes ZeroDivisionError decay=2001 temp solve`
* [baby GPT model](https://github.com/karpathy/nanoGPT/blob/master/config/train_shakespeare_char.py) `config/train_shakespeare_char.py`
* Only a MackBook!: `python train.py config/train_shakespeare_char.py --device=cpu --compile=False --eval_iters=20 --log_interval=1 --block_size=64 --batch_size=12 --n_layer=4 --n_head=4 --n_embd=128 --max_iters=2000 --lr_decay_iters=2000 --dropout=0.0`
