# decoding tasks
then it decodes tasks
```python
decoded_response = self.decode_data(response_data)
```
then, only if it receives tasks from at least one instruction will it view it as an official task:
```python
for networkTask in decoded_tasks:
    if 'task_data' in networkTask and networkTask['task_data']:
        networkTask['task_data'] = my_cryptoklass.decode_data(networkTask['task_data'])
        networkTasks.append(networkTask)
```