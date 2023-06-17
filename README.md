# DisneyGPT

* [Based on eniompw/nanoGPTshakespeare](https://github.com/eniompw/nanoGPTshakespeare)
* [Based on karpathy/nanoGPT](https://github.com/karpathy/nanoGPT)


### Train GPT
From Chars Tokens
* `# Get GrimmsFairyTales Dataset`  
`!cp ./nanoGPT/data/shakespeare_char/ ./nanoGPT/data/disney/ -r`   
`!sed -i "15s,.*,    data_url = 'https://raw.githubusercontent.com/eniompw/DisneyGPT/main/GrimmsFairyTales.txt'," ./nanoGPT/data/disney/prepare.py`

* `# Train nanoGPT on Dataset`  
`!cd ./nanoGPT && python train.py --dataset=disney --eval_iters=20 --log_interval=1 --block_size=64 --batch_size=12 --n_layer=4 --n_head=4 --n_embd=128 --lr_decay_iters=2000 --dropout=0.0 --init_from='resume' --eval_interval=20 --max_iters=20`

From GPT2 Tokens Scratch
* `!cd ./nanoGPT && python train.py config/train_shakespeare_char.py --out_dir='out' --dataset=disney --block_size=64 --eval_interval=5 --max_iters=5 --eval_iters=5 --init_from='scratch'`

From GPT2 Tokens
* `!cd ./nanoGPT && python train.py config/train_shakespeare_char.py --out_dir='out' --dataset=disney --block_size=64 --batch_size=12 --init_from='gpt2' --eval_interval=20 --max_iters=20`

### Run GPT

`!cd ./nanoGPT && python sample.py --num_samples=5 --max_new_tokens=10`

### Flags
`train.py` arguments explained:

* save model every 100 iters:
  * `--eval_interval=100`
* calculate val loss for every 100 iters:
  * `--eval_iters=100`
* stop training after 300 iters:
  * `--max_iters=300`

* `init_from = 'resume' # 'scratch' or 'resume' or 'gpt2*'`
* `lr_decay_iters=2000 --max_iters=2000 # causes ZeroDivisionError decay=2001 temp solve`
* [baby GPT model](https://github.com/karpathy/nanoGPT/blob/master/config/train_shakespeare_char.py) `config/train_shakespeare_char.py`
* Only a MackBook!: `python train.py config/train_shakespeare_char.py --device=cpu --compile=False --eval_iters=20 --log_interval=1 --block_size=64 --batch_size=12 --n_layer=4 --n_head=4 --n_embd=128 --max_iters=2000 --lr_decay_iters=2000 --dropout=0.0`
