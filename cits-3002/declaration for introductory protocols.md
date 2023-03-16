
- can represent each data link frame as a structure in programming languages that support a byte datatype 
- premit a program to access/copy these bytes using their memory addresses
- the frame will consist of a header section and the actual data to be sent

```
#define  MAX_DATA_SIZE        1000

typedef struct {
// firstly, the frame's header_
    int       len;            // length of the payload, only

// followed by the payload
    **char**      data[MAX_DATA_SIZE];
} FRAME;

#define FRAME_HEADER_SIZE     (sizeof(FRAME) - sizeof(FRAME.data))

#define FRAME_SIZE(f)         (FRAME_HEADER_SIZE + f.len)
```