# 命令行工具

## Fire

[Fire Docs](https://github.com/google/python-fire)

```py
import fire

def action_a():
    pass

def action_b(arg1):
    pass

def main():
    fire.Fire(
        "action-a": action_a,
        "action-b": action_b
    )

if __name__ == '__main__':
    main()
```
