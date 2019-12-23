<!--

#################################################
### THIS FILE WAS AUTOGENERATED! DO NOT EDIT! ###
#################################################
# file to edit: nbs/index.ipynb
# command to build the docs after a change: nbdev_build_docs

-->

# Video Utilities for OpenCV

> `videoutils` lets you get rid of writing boilerplate code for reading video and adds some convenience on top of that.


## Install

`pip install videoutils`

## How to use
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
from videoutils.io import read_video, as_tensor
fname = 'files/interstellar-waves-edit.mp4'
```

</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
x = read_video(fname)
len(x)
x[0].shape
```

</div>
<div class="output_area" markdown="1">




    1578






    (480, 720, 3)



</div>

</div>

By default, `read_video` returns a list of `np.array`s of shape `(height, width, channels)`. <br>
However, you can define precisely which frames you'd like to grab in a number of ways. This is done by using either the {`start_idx`, `end_idx`, `frame_stride`} or `target_frames` arguments. 

### Grab the first `n` frames
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
n = 50
x  = read_video(fname, end_idx=n)
x2 = read_video(fname, target_frames=(0,n))

len(x)
len(x) == len(x2)
```

</div>
<div class="output_area" markdown="1">




    50






    True



</div>

</div>

### Grab every `n`th frame
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
n=5
x = read_video(fname, frame_stride=n, end_idx=50)
len(x)
```

</div>
<div class="output_area" markdown="1">




    10



</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
x = read_video(fname, frame_stride=5) # total frames = 1578
len(x)
```

</div>
<div class="output_area" markdown="1">




    316



</div>

</div>

### Grab frames at specific indices
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
x = read_video(fname, target_frames=[10, 50, 76, 420])
len(x)
```

</div>
<div class="output_area" markdown="1">




    4



</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
x  = read_video(fname, start_idx=10, end_idx=15)
x2 = read_video(fname, target_frames=(10, 15))

len(x)
len(x) == len(x2)
```

</div>
<div class="output_area" markdown="1">




    5






    True



</div>

</div>

### Return as `torch.Tensor`

You can pass any function that transforms a `np.array` of shape `(height, width, channels)` to the `apply` argument. `Videoutils` provides `as_tensor` and `as_normalised_tensor` for convenience 
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
x  = read_video(fname, end_idx=10, apply=as_tensor)
x2 = read_video(fname, end_idx=10, apply=as_normalised_tensor)

x.shape
x.shape == x2.shape
x.mean(), x2.mean()
```

</div>
<div class="output_area" markdown="1">




    torch.Size([10, 3, 480, 720])






    True






    (tensor(36.8276), tensor(0.1444))



</div>

</div>
