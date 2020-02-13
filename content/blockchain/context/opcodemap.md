### 常数指令
关键字 | 值（十六进制） | 描述
---|---|---
PUSH0 | 0x00 | 向计算栈中压入一个长度为 0 的字节数组
PUSHF | 0x00 | 向计算栈中压入一个长度为 0 的字节数组
PUSHBYTES1-75 | 0x01-0x4B | 向计算栈中压入一个字节数组，其长度等于本指令字节码的数值
PUSHDATA1 | 0x4C | 向计算栈中压入一个字节数组，其长度由本指令后的 1|2|4 字节指定
PUSHDATA2 | 0x4D | 向计算栈中压入一个字节数组，其长度由本指令后的 1|2|4 字节指定
PUSHDATA4 | 0x4E | 向计算栈中压入一个字节数组，其长度由本指令后的 1|2|4 字节指定
PUSHM1 | 0x4F | 向计算栈中压入一个大整数，其数值等于-1
PUSH1-16 | 0x51-0x60 | 向计算栈中压入一个大整数，其数值等于 1~16
PUSHT | 0x51 | 向计算栈中压入一个大整数，其数值等于 1

### 逻辑控制指令
关键字 | 值（十六进制） | 描述
---|---|---
NOP | 0x61 | 没有任何额外的功能，但是会使指令计步器加 1
JMP | 0x62 | 无条件跳转到指定偏移位置，偏移量由本指令后的 2 字节指定
JMPIF | 0x63 | 当计算栈栈顶元素不等于 0 时，跳转到指定偏移位置，偏移量由本指令后的2字节指定。不论条件判断成功与否，栈顶元素将被移除
JMPIFNOT | 0x64 | 当计算栈栈顶元素等于 0 时，跳转到指定偏移位置，偏移量由本指令后的 2 字节指定。不论条件判断成功与否，栈顶元素将被移除
CALL | 0x65 | 调用指定偏移位置的函数，偏移量由本指令后的 2 字节指定
RET | 0x66 | 移除调用栈的顶部元素，并使程序在调用栈的下一帧中继续执行。如果调用栈为空，则虚拟机进入停机状态
APPCALL | 0x67 | 调用指定地址的函数，函数地址由本指令后的 20 字节指定
SYSCALL | 0x68 | 调用指定的互操作函数，函数名称由本指令后的字符串指定
TAILCALL | 0x69 | 以尾调用的方式，调用指定的互操作函数，函数名称由本指令后的字符串指定

### 栈操作指令
关键字 | 值（十六进制） | 描述
---|---|---|
DUPFROMALTSTACK | 0x6A | ??
TOALTSTACK | 0x6B | 移除计算栈栈顶的元素，并将其压入备用栈
FROMALTSTACK | 0x6C | 移除备用栈栈顶的元素，并将其压入计算栈
XDROP | 0x6D | 移除计算栈栈顶的元素 n，并移除剩余的索引为 n 的元素
XSWAP | 0x72 | 移除计算栈栈顶的元素 n，并将剩余的索引为 0 的元素和索引为 n 的元素交换位置
XTUCK | 0x73 | 移除计算栈栈顶的元素 n，并将剩余的索引为 0 的元素复制并插入到索引为 n的位置
DEPTH | 0x74 | 将当前计算栈中的元素数量压入计算栈顶
DROP | 0x75 | 移除计算栈栈顶的元素
DUP | 0x76 | 复制计算栈栈顶的元素
NIP | 0x77 | 移除计算栈栈顶的第 2 个元素
OVER | 0x78 | 复制计算栈栈顶的第二个元素，并压入栈顶
PICK | 0x79 | 移除计算栈栈顶的元素 n，并将索引为 n 的元素复制到栈顶
ROLL | 0x7A | 移除计算栈栈顶的元素 n，并将索引为 n 的元素移动到栈顶
ROT | 0x7B | 移除计算栈栈顶的第 3 个元素，并将其压入栈顶
SWAP | 0x7C | 交换计算栈栈顶两个元素的位置
TUCK | 0x7D | 复制计算栈栈顶的元素到索引为 2 的位置

### 字符串指令
关键字 | 值（十六进制） | 描述
---|---|---
CAT | 0x7E | 移除计算栈栈顶的两个元素，并将其拼接后压入栈顶
SUBSTR | 0x7F | 移除计算栈栈顶的三个元素，取子串后压入栈顶
LEFT | 0x80 | 移除计算栈栈顶的两个元素，取子串后压入栈顶
RIGHT | 0x81 | 移除计算栈栈顶的两个元素，取子串后压入栈顶
SIZE | 0x82 | 将计算栈栈顶元素的长度压入栈顶

### 逻辑运算指令
关键字 | 值（十六进制） | 描述
---|---|---
INVERT | 0x83 | 对计算栈栈顶的元素按位取反
AND | 0x84 | 对计算栈栈顶的两个元素执行按位与运算
OR | 0x85 | 对计算栈栈顶的两个元素执行按位或运算
XOR | 0x86 | 对计算栈栈顶的两个元素执行按位异或运算
EQUAL | 0x87 | 对计算栈栈顶的两个元素执行逐字节的相等判断

### 算数运算指令
关键字 | 值（十六进制） | 描述
---|---|---
INC | 0x8B | 对计算栈栈顶的大整数执行递增运算
DEC | 0x8C | 对计算栈栈顶的大整数执行递减运算
SAL | 0x8D | 对计算栈栈顶的大整数执行乘以 2 的运算
SAR | 0x8E | 对计算栈栈顶的大整数执行除以 2 的运算
NEGATE | 0x8F | 求计算栈栈顶的大整数的相反数
ABS | 0x90 | 求计算栈栈顶的大整数的绝对值
NOT | 0x91 | 对计算栈栈顶的元素执行逻辑非运算
NZ | 0x92 | 判断计算栈栈顶的大整数是否为非 0 值
ADD | 0x93 | 对计算栈栈顶的两个大整数执行加法运算
SUB | 0x94 | 对计算栈栈顶的两个大整数执行减法运算
MUL | 0x95 | 对计算栈栈顶的两个大整数执行乘法运算
DIV | 0x96 | 对计算栈栈顶的两个大整数执行除法运算
MOD | 0x97 | 对计算栈栈顶的两个大整数执行求余运算
SHL | 0x98 | 对计算栈中的大整数执行左移运算
SHR | 0x99 | 对计算栈中的大整数执行右移运算
BOOLAND | 0x9A | 对计算栈栈顶的两个元素执行逻辑与运算
BOOLOR | 0x9B | 对计算栈栈顶的两个元素执行逻辑或运算
NUMEQUAL | 0x9C | 对计算栈栈顶的两个大整数执行相等判断
NUMNOTEQUAL | 0x9E | 对计算栈栈顶的两个大整数执行不相等判断
LT | 0x9F | 对计算栈栈顶的两个大整数执行小于判断
GT | 0xA0 | 对计算栈栈顶的两个大整数执行大于判断
LTE | 0xA1 | 对计算栈栈顶的两个大整数执行小于等于判断
GTE | 0xA2 | 对计算栈栈顶的两个大整数执行大于等于判断
MIN | 0xA3 | 取出计算栈栈顶的两个大整数中的最小值
MAX | 0xA4 | 取出计算栈栈顶的两个大整数中的最大值
WITHIN | 0xA5 | 判断计算栈中的大整数是否在指定的数值范围内

### 密码学指令
关键字 | 值（十六进制） | 描述
---|---|---
SHA1 | 0xA7 | 对计算栈栈顶的元素执行 SHA1 运算
SHA256 | 0xA8 | 对计算栈栈顶的元素执行 SHA256 运算
HASH160 | 0xA9 | 对计算栈栈顶的元素执行内置的 160 位散列运算
HASH256 | 0xAA | 对计算栈栈顶的元素执行内置的 256 位散列运算
CHECKSIG | 0xAC | 利用计算栈栈顶元素中的签名和公钥，对当前验证对象执行内置的非对称签名验证操作
VERIFY | 0xAD | ??
CHECKMULTISIG | 0xAE | 利用计算栈栈顶元素中的多个签名和公钥，对当前验证对象执行内置的非对称多重签名验证操作

### 高级数据结构指令(数组、结构、映射)
关键字 | 值（十六进制） | 描述
---|---|---
ARRAYSIZE | 0xC0 | 获取计算栈栈顶的数组的元素数量
PACK | 0xC1 | 将计算栈栈顶的 n 个元素打包成数组
UNPACK | 0xC2 | 将计算栈栈顶的数组拆包成元素序列
PICKITEM | 0xC3 | 获取计算栈栈顶的数组中的指定元素
SETITEM | 0xC4 | ??
NEWARRAY | 0xC5 | ??
NEWSTRUCT | 0xC6 | ??
NEWMAP | 0xC7 | ??
APPEND | 0xC8 | ??
REVERSE | 0xC9 | ??
REMOVE | 0xCA | ??
HASKEY | 0xCB | ??
KEYS | 0xCC | ??
VALUES | 0xCD | ??

### 堆栈隔离
关键字 | 值（十六进制） | 描述
---|---|---
CALLI | 0xE0 | ??
CALLE | 0xE1 | ??
CALLED | 0xE2 | ??
CALLET | 0xE3 | ??
CALLEDT | 0xE4 | ??

### 异常
关键字 | 值（十六进制） | 描述
---|---|---
THROW | 0xF0 | ??
THROWIFNOT | 0xF1 | ??

### 解析opcode代码参考
```
func (self *Executor) ExecuteOp(opcode OpCode, context *ExecutionContext) (VMState, error) {
	if err := self.checkFeaturesEnabled(opcode); err != nil {
		return FAULT, err
	}

	if opcode >= PUSHBYTES1 && opcode <= PUSHBYTES75 {
		buf, err := context.OpReader.ReadBytes(int(opcode))
		if err != nil {
			return FAULT, err
		}
		val, err := types.VmValueFromBytes(buf)
		if err != nil {
			return FAULT, err
		}
		err = self.EvalStack.Push(val)
		if err != nil {
			return FAULT, err
		}
		return NONE, nil
	}

	switch opcode {
	case PUSH0:
		err := self.EvalStack.Push(types.VmValueFromInt64(0))
		if err != nil {
			return FAULT, err
		}
	case PUSHDATA1, PUSHDATA2, PUSHDATA4:
		var numBytes int
		if opcode == PUSHDATA1 {
			d, err := context.OpReader.ReadByte()
			if err != nil {
				return FAULT, err
			}

			numBytes = int(d)
		} else if opcode == PUSHDATA2 {
			num, err := context.OpReader.ReadUint16()
			if err != nil {
				return FAULT, err
			}
			numBytes = int(num)
		} else {
			num, err := context.OpReader.ReadUint32()
			if err != nil {
				return FAULT, err
			}
			numBytes = int(num)
		}

		data, err := context.OpReader.ReadBytes(numBytes)
		if err != nil {
			return FAULT, err
		}
		val, err := types.VmValueFromBytes(data)
		if err != nil {
			return FAULT, err
		}
		err = self.EvalStack.Push(val)
		if err != nil {
			return FAULT, err
		}
	case PUSHM1, PUSH1, PUSH2, PUSH3, PUSH4, PUSH5, PUSH6, PUSH7, PUSH8, PUSH9, PUSH10, PUSH11, PUSH12, PUSH13, PUSH14, PUSH15, PUSH16:
		val := int64(opcode) - int64(PUSH1) + 1
		err := self.EvalStack.Push(types.VmValueFromInt64(val))
		if err != nil {
			return FAULT, err
		}
		// Flow control
	case NOP:
		return NONE, nil
	case JMP, JMPIF, JMPIFNOT, CALL:
		if opcode == CALL {
			caller := context.Clone()
			err := caller.SetInstructionPointer(int64(caller.GetInstructionPointer() + 2))
			if err != nil {
				return FAULT, err
			}
			err = self.PushContext(caller)
			if err != nil {
				return FAULT, err
			}
			opcode = JMP
		}

		num, err := context.OpReader.ReadInt16()
		if err != nil {
			return FAULT, err
		}
		offset := int(num)
		offset = context.GetInstructionPointer() + offset - 3

		if offset < 0 || offset > len(context.Code) {
			return FAULT, errors.ERR_FAULT
		}
		var needJmp = true
		if opcode != JMP {
			val, err := self.EvalStack.PopAsBool()
			if err != nil {
				return FAULT, err
			}
			if opcode == JMPIF {
				needJmp = val
			} else {
				needJmp = !val
			}
		}

		if needJmp {
			err := context.SetInstructionPointer(int64(offset))
			if err != nil {
				return FAULT, err
			}
		}
	case DCALL:
		caller := context.Clone()
		err := self.PushContext(caller)
		if err != nil {
			return FAULT, errors.ERR_OVER_STACK_LEN
		}
		target, err := self.EvalStack.PopAsInt64()
		if err != nil {
			return FAULT, err
		}
		if target < 0 || target >= int64(len(self.Context.Code)) {
			return FAULT, errors.ERR_DCALL_OFFSET_ERROR
		}
		err = self.Context.SetInstructionPointer(target)
		if err != nil {
			return FAULT, err
		}
	case RET:
		// omit handle error is ok, if context stack is empty, self.Context will be nil
		// which will be checked outside before the next opcode call
		self.Context, _ = self.PopContext()
	case DUPFROMALTSTACK:
		val, err := self.AltStack.Peek(0)
		if err != nil {
			return FAULT, err
		}
		err = self.EvalStack.Push(val)
		if err != nil {
			return FAULT, err
		}
	case TOALTSTACK:
		val, err := self.EvalStack.Pop()
		if err != nil {
			return FAULT, err
		}
		err = self.AltStack.Push(val)
		if err != nil {
			return FAULT, err
		}
	case FROMALTSTACK:
		val, err := self.AltStack.Pop()
		if err != nil {
			return FAULT, err
		}
		err = self.EvalStack.Push(val)
		if err != nil {
			return FAULT, err
		}

	case XDROP: // XDROP is zero based
		n, err := self.EvalStack.PopAsInt64()
		if err != nil {
			return FAULT, err
		}
		_, err = self.EvalStack.Remove(n)
		if err != nil {
			return FAULT, err
		}
	case XSWAP:
		n, err := self.EvalStack.PopAsInt64()
		if err != nil {
			return FAULT, err
		}

		err = self.EvalStack.Swap(0, n)
		if err != nil {
			return FAULT, err
		}
	case XTUCK:
		n, err := self.EvalStack.PopAsInt64()
		if err != nil {
			return FAULT, err
		}

		val, err := self.EvalStack.Peek(0)
		if err != nil {
			return FAULT, err
		}

		err = self.EvalStack.Insert(n, val)
		if err != nil {
			return FAULT, err
		}
	case DEPTH:
		err := self.EvalStack.PushInt64(int64(self.EvalStack.Count()))
		if err != nil {
			return FAULT, err
		}
	case DROP:
		_, err := self.EvalStack.Pop()
		if err != nil {
			return FAULT, err
		}
	case DUP:
		val, err := self.EvalStack.Peek(0)
		if err != nil {
			return FAULT, err
		}
		err = self.EvalStack.Push(val)
		if err != nil {
			return FAULT, err
		}
	case NIP:
		_, val, err := self.EvalStack.PopPair()
		if err != nil {
			return FAULT, err
		}

		err = self.EvalStack.Push(val)
		if err != nil {
			return FAULT, err
		}
	case OVER:
		val, err := self.EvalStack.Peek(1)
		if err != nil {
			return FAULT, err
		}

		err = self.EvalStack.Push(val)
		if err != nil {
			return FAULT, err
		}
	case PICK:
		n, err := self.EvalStack.PopAsInt64()
		if err != nil {
			return FAULT, err
		}

		val, err := self.EvalStack.Peek(n)
		if err != nil {
			return FAULT, err
		}

		err = self.EvalStack.Push(val)
		if err != nil {
			return FAULT, err
		}
	case ROLL, ROT:
		var n int64
		var err error
		if opcode == ROT {
			n = 2
		} else {
			n, err = self.EvalStack.PopAsInt64()
			if err != nil {
				return FAULT, err
			}
		}

		// need clearly define the behave when n == 0 and stack is empty
		val, err := self.EvalStack.Remove(n)
		if err != nil {
			return FAULT, err
		}

		err = self.EvalStack.Push(val)
		if err != nil {
			return FAULT, err
		}
	case SWAP: // The top two items on the stack are swapped.
		err := self.EvalStack.Swap(0, 1)
		if err != nil {
			return FAULT, err
		}
	case TUCK: // The item at the top of the stack is copied and inserted before the second-to-top item.
		x1, x2, err := self.EvalStack.PopPair()
		if err != nil {
			return FAULT, err
		}

		err = self.EvalStack.PushMany(x2, x1, x2)
		if err != nil {
			return FAULT, err
		}
		// Splice
	case CAT:
		left, right, err := self.EvalStack.PopPairAsBytes()
		if err != nil {
			return FAULT, err
		}

		val := make([]byte, 0, len(left)+len(right))
		val = append(val, left...)
		val = append(val, right...)
		err = self.EvalStack.PushBytes(val)
		if err != nil {
			return FAULT, err
		}
	case SUBSTR:
		start, count, err := self.EvalStack.PopPairAsInt64()
		if err != nil {
			return FAULT, err
		}
		arr, err := self.EvalStack.PopAsBytes()
		if err != nil {
			return FAULT, err
		}

		length := int64(len(arr))
		if start < 0 || start > length {
			return FAULT, errors.ERR_OVER_MAX_ARRAY_SIZE
		}
		if count < 0 || count > length {
			return FAULT, errors.ERR_OVER_MAX_ARRAY_SIZE
		}
		end := start + count
		if end > length {
			return FAULT, errors.ERR_OVER_MAX_ARRAY_SIZE
		}

		b := arr[start:end]
		err = self.EvalStack.PushBytes(b)
		if err != nil {
			return FAULT, err
		}

	case LEFT:
		count, err := self.EvalStack.PopAsInt64()
		if err != nil {
			return FAULT, err
		}
		arr, err := self.EvalStack.PopAsBytes()
		if err != nil {
			return FAULT, err
		}

		length := int64(len(arr))
		if count < 0 || count > length {
			return FAULT, errors.ERR_OVER_MAX_ARRAY_SIZE
		}

		b := arr[:count]
		err = self.EvalStack.PushBytes(b)
		if err != nil {
			return FAULT, err
		}
	case RIGHT:
		count, err := self.EvalStack.PopAsInt64()
		if err != nil {
			return FAULT, err
		}
		arr, err := self.EvalStack.PopAsBytes()
		if err != nil {
			return FAULT, err
		}

		length := int64(len(arr))
		if count < 0 || count > length {
			return FAULT, errors.ERR_OVER_MAX_ARRAY_SIZE
		}

		b := arr[length-count:]
		err = self.EvalStack.PushBytes(b)
		if err != nil {
			return FAULT, err
		}
	case SIZE:
		arr, err := self.EvalStack.PopAsBytes()
		if err != nil {
			return FAULT, err
		}

		err = self.EvalStack.PushInt64(int64(len(arr)))
		if err != nil {
			return FAULT, err
		}
	// Bitwise logic
	case INVERT:
		left, err := self.EvalStack.PopAsIntValue()
		if err != nil {
			return FAULT, err
		}
		val := left.Not()
		err = self.EvalStack.Push(types.VmValueFromIntValue(val))
		if err != nil {
			return FAULT, err
		}
	case AND, OR, XOR:
		left, right, err := self.EvalStack.PopPairAsIntVal()
		if err != nil {
			return FAULT, err
		}

		var val types.IntValue
		switch opcode {
		case AND:
			val, err = left.And(right)
		case OR:
			val, err = left.Or(right)
		case XOR:
			val, err = left.Xor(right)
		default:
			panic("unreachable")
		}
		if err != nil {
			return FAULT, err
		}
		err = self.EvalStack.Push(types.VmValueFromIntValue(val))
		if err != nil {
			return FAULT, err
		}
	case EQUAL:
		left, right, err := self.EvalStack.PopPair()
		if err != nil {
			return FAULT, err
		}
		err = self.EvalStack.PushBool(left.Equals(right))
		if err != nil {
			return FAULT, err
		}
	case INC, DEC, SIGN, NEGATE, ABS:
		x, err := self.EvalStack.PopAsIntValue()
		if err != nil {
			return FAULT, err
		}

		var val types.IntValue
		switch opcode {
		case INC:
			val, err = x.Add(types.IntValFromInt(1))
		case DEC:
			val, err = x.Sub(types.IntValFromInt(1))
		case SIGN:
			cmp := x.Cmp(types.IntValFromInt(0))
			val = types.IntValFromInt(int64(cmp))
		case NEGATE:
			val, err = types.IntValFromInt(0).Sub(x)
		case ABS:
			val = x.Abs()
		default:
			panic("unreachable")
		}
		if err != nil {
			return FAULT, err
		}

		err = self.EvalStack.Push(types.VmValueFromIntValue(val))
		if err != nil {
			return FAULT, err
		}
	case NZ:
		x, err := self.EvalStack.PopAsIntValue()
		if err != nil {
			return FAULT, err
		}

		cmp := x.Cmp(types.IntValFromInt(0))
		if cmp == 0 {
			err = self.EvalStack.PushBool(false)
		} else {
			err = self.EvalStack.PushBool(true)
		}

		if err != nil {
			return FAULT, err
		}
	case ADD, SUB, MUL, DIV, MOD, MAX, MIN:
		left, right, err := self.EvalStack.PopPairAsIntVal()
		if err != nil {
			return FAULT, err
		}
		var val types.IntValue
		switch opcode {
		case ADD:
			val, err = left.Add(right)
		case SUB:
			val, err = left.Sub(right)
		case MUL:
			val, err = left.Mul(right)
		case DIV:
			val, err = left.Div(right)
		case MOD:
			val, err = left.Mod(right)
		case MAX:
			val, err = left.Max(right)
		case MIN:
			val, err = left.Min(right)
		default:
			panic("unreachable")
		}
		if err != nil {
			return FAULT, err
		}
		err = self.EvalStack.Push(types.VmValueFromIntValue(val))
		if err != nil {
			return FAULT, err
		}
	case SHL, SHR:
		x2, err := self.EvalStack.PopAsIntValue()
		if err != nil {
			return FAULT, err
		}
		x1, err := self.EvalStack.PopAsIntValue()
		if err != nil {
			return FAULT, err
		}
		var res types.IntValue
		switch opcode {
		case SHL:
			res, err = x1.Lsh(x2)
			if err != nil {
				return FAULT, err
			}
		case SHR:
			res, err = x1.Rsh(x2)
			if err != nil {
				return FAULT, err
			}
		default:
			panic("unreachable")
		}
		b := types.VmValueFromIntValue(res)
		err = self.EvalStack.Push(b)
		if err != nil {
			return FAULT, err
		}
	case NUMNOTEQUAL, NUMEQUAL:
		// note : pop as bytes to avoid hard-fork because previous version missing check
		// whether the params are a valid 32 byte integer
		left, right, err := self.EvalStack.PopPairAsBytes()
		if err != nil {
			return FAULT, err
		}
		l := common.BigIntFromNeoBytes(left)
		r := common.BigIntFromNeoBytes(right)
		var val bool
		switch opcode {
		case NUMEQUAL:
			val = l.Cmp(r) == 0
		case NUMNOTEQUAL:
			val = l.Cmp(r) != 0
		default:
			panic("unreachable")
		}
		err = self.EvalStack.PushBool(val)
		if err != nil {
			return FAULT, err
		}
	case LT, GT, LTE, GTE:
		leftVal, rightVal, err := self.EvalStack.PopPair()
		if err != nil {
			return FAULT, err
		}
		left, err := leftVal.AsBigInt()
		if err != nil {
			return FAULT, err
		}
		right, err := rightVal.AsBigInt()
		if err != nil {
			return FAULT, err
		}
		var val bool
		switch opcode {
		case LT:
			val = left.Cmp(right) < 0
		case GT:
			val = left.Cmp(right) > 0
		case LTE:
			val = left.Cmp(right) <= 0
		case GTE:
			val = left.Cmp(right) >= 0
		default:
			panic("unreachable")
		}
		if err != nil {
			return FAULT, err
		}
		err = self.EvalStack.PushBool(val)
		if err != nil {
			return FAULT, err
		}

	case BOOLAND, BOOLOR:
		left, right, err := self.EvalStack.PopPairAsBool()
		if err != nil {
			return FAULT, err
		}

		var val bool
		switch opcode {
		case BOOLAND:
			val = left && right
		case BOOLOR:
			val = left || right
		default:
			panic("unreachable")
		}
		err = self.EvalStack.PushBool(val)
		if err != nil {
			return FAULT, err
		}
	case NOT:
		x, err := self.EvalStack.PopAsBool()
		if err != nil {
			return FAULT, err
		}

		err = self.EvalStack.PushBool(!x)
		if err != nil {
			return FAULT, err
		}
	case WITHIN:
		val, left, right, err := self.EvalStack.PopTripleAsIntVal()
		if err != nil {
			return FAULT, err
		}
		v1 := val.Cmp(left)
		v2 := val.Cmp(right)

		err = self.EvalStack.PushBool(v1 >= 0 && v2 < 0)
		if err != nil {
			return FAULT, err
		}
	case SHA1, SHA256, HASH160, HASH256:
		x, err := self.EvalStack.PopAsBytes()
		if err != nil {
			return FAULT, err
		}

		var hash []byte
		switch opcode {
		case SHA1:
			sh := sha1.New()
			sh.Write(x)
			hash = sh.Sum(nil)
		case SHA256:
			sh := sha256.New()
			sh.Write(x)
			hash = sh.Sum(nil)
		case HASH160:
			temp := sha256.Sum256(x)
			md := ripemd160.New()
			md.Write(temp[:])
			hash = md.Sum(nil)
		case HASH256:
			temp := sha256.Sum256(x)
			data := sha256.Sum256(temp[:])
			hash = data[:]
		}
		val, err := types.VmValueFromBytes(hash)
		if err != nil {
			return FAULT, err
		}
		err = self.EvalStack.Push(val)
		if err != nil {
			return FAULT, err
		}
	case VERIFY:
		pub, sig, data, err := self.EvalStack.PopTripleAsBytes()
		if err != nil {
			return FAULT, err
		}

		key, err := keypair.DeserializePublicKey(pub)
		if err != nil {
			return FAULT, err
		}

		verErr := signature.Verify(key, data, sig)
		err = self.EvalStack.PushBool(verErr == nil)
		if err != nil {
			return FAULT, err
		}
	// Array
	case ARRAYSIZE:
		val, err := self.EvalStack.Pop()
		if err != nil {
			return FAULT, err
		}

		var length int64
		if array, err := val.AsArrayValue(); err == nil {
			length = array.Len()
		} else if buf, err := val.AsBytes(); err == nil {
			length = int64(len(buf))
		} else {
			return FAULT, errors.ERR_BAD_TYPE
		}

		err = self.EvalStack.PushInt64(length)
		if err != nil {
			return FAULT, err
		}
	case PACK:
		size, err := self.EvalStack.PopAsInt64()
		if err != nil {
			return FAULT, err
		}
		if size < 0 {
			return FAULT, errors.ERR_BAD_VALUE
		}
		array := types.NewArrayValue()
		for i := int64(0); i < size; i++ {
			val, err := self.EvalStack.Pop()
			if err != nil {
				return FAULT, err
			}

			err = array.Append(val)
			if err != nil {
				return FAULT, err
			}
		}
		err = self.EvalStack.Push(types.VmValueFromArrayVal(array))
		if err != nil {
			return FAULT, err
		}
	case UNPACK:
		arr, err := self.EvalStack.PopAsArray()
		if err != nil {
			return FAULT, err
		}
		l := len(arr.Data)
		for i := l - 1; i >= 0; i-- {
			err = self.EvalStack.Push(arr.Data[i])
			if err != nil {
				return FAULT, err
			}
		}
		err = self.EvalStack.PushInt64(int64(l))
		if err != nil {
			return FAULT, err
		}
	case PICKITEM:
		item, index, err := self.EvalStack.PopPair()
		if err != nil {
			return FAULT, err
		}

		var val types.VmValue
		if array, err := item.AsArrayValue(); err == nil {
			ind, err := index.AsInt64()
			if err != nil {
				return FAULT, err
			}
			if ind < 0 || ind >= array.Len() {
				return FAULT, errors.ERR_INDEX_OUT_OF_BOUND
			}

			val = array.Data[ind]
		} else if struc, err := item.AsStructValue(); err == nil {
			ind, err := index.AsInt64()
			if err != nil {
				return FAULT, err
			}
			if ind < 0 || ind >= struc.Len() {
				return FAULT, errors.ERR_INDEX_OUT_OF_BOUND
			}
			val = struc.Data[ind]
		} else if mapVal, err := item.AsMapValue(); err == nil {
			value, ok, err := mapVal.Get(index)
			if err != nil {
				return FAULT, err
			} else if ok == false {
				// todo: suply a nil value in vm?
				return FAULT, errors.ERR_MAP_NOT_EXIST
			}
			val = value
		} else if buf, err := item.AsBytes(); err == nil {
			ind, err := index.AsInt64()
			if err != nil {
				return FAULT, err
			}
			if ind < 0 || ind >= int64(len(buf)) {
				return FAULT, errors.ERR_INDEX_OUT_OF_BOUND
			}
			val = types.VmValueFromInt64(int64(buf[ind]))
		} else {
			return FAULT, errors.ERR_BAD_TYPE
		}

		err = self.EvalStack.Push(val)
		if err != nil {
			return FAULT, err
		}

	case SETITEM:
		//todo: the original implementation for Struct type may have problem.
		item, index, val, err := self.EvalStack.PopTriple()
		if err != nil {
			return FAULT, err
		}
		if s, err := val.AsStructValue(); err == nil {
			t, err := s.Clone()
			if err != nil {
				return FAULT, err
			}
			val = types.VmValueFromStructVal(t)
		}
		if array, err := item.AsArrayValue(); err == nil {
			ind, err := index.AsInt64()
			if err != nil {
				return FAULT, err
			}
			if ind < 0 || ind >= array.Len() {
				return FAULT, errors.ERR_INDEX_OUT_OF_BOUND
			}

			array.Data[ind] = val
		} else if struc, err := item.AsStructValue(); err == nil {
			ind, err := index.AsInt64()
			if err != nil {
				return FAULT, err
			}
			if ind < 0 || ind >= struc.Len() {
				return FAULT, errors.ERR_INDEX_OUT_OF_BOUND
			}

			struc.Data[ind] = val
		} else if mapVal, err := item.AsMapValue(); err == nil {
			err = mapVal.Set(index, val)
			if err != nil {
				return FAULT, err
			}
		} else {
			return FAULT, errors.ERR_BAD_TYPE
		}
	case NEWARRAY:
		count, err := self.EvalStack.PopAsInt64()
		if err != nil {
			return FAULT, err
		}
		if count < 0 || count > MAX_ARRAY_SIZE {
			return FAULT, errors.ERR_BAD_VALUE
		}
		array := types.NewArrayValue()
		for i := int64(0); i < count; i++ {
			err = array.Append(types.VmValueFromBool(false))
			if err != nil {
				return FAULT, err
			}
		}
		err = self.EvalStack.Push(types.VmValueFromArrayVal(array))
		if err != nil {
			return FAULT, err
		}
	case NEWSTRUCT:
		count, err := self.EvalStack.PopAsInt64()
		if err != nil {
			return FAULT, err
		}
		if count < 0 || count > MAX_ARRAY_SIZE {
			return FAULT, errors.ERR_BAD_VALUE
		}
		array := types.NewStructValue()
		for i := int64(0); i < count; i++ {
			err = array.Append(types.VmValueFromBool(false))
			if err != nil {
				return FAULT, err
			}
		}
		err = self.EvalStack.Push(types.VmValueFromStructVal(array))
		if err != nil {
			return FAULT, err
		}
	case NEWMAP:
		err := self.EvalStack.Push(types.NewMapVmValue())
		if err != nil {
			return FAULT, err
		}
	case APPEND:
		item, err := self.EvalStack.Pop()
		if err != nil {
			return FAULT, err
		}
		if s, err := item.AsStructValue(); err == nil {
			t, err := s.Clone()
			if err != nil {
				return FAULT, err
			}
			item = types.VmValueFromStructVal(t)
		}
		val, err := self.EvalStack.Pop()
		switch val.GetType() {
		case types.StructType:
			array, _ := val.AsStructValue()
			err = array.Append(item)
			if err != nil {
				return FAULT, err
			}
		case types.ArrayType:
			array, _ := val.AsArrayValue()
			err = array.Append(item)
			if err != nil {
				return FAULT, err
			}
		default:
			return FAULT, fmt.Errorf("[executor] ExecuteOp APPEND error, unknown datatype")
		}
	case REVERSE:
		var data []types.VmValue
		item, err := self.EvalStack.Pop()
		if err != nil {
			return FAULT, err
		}
		if array, err := item.AsArrayValue(); err == nil {
			data = array.Data
		} else if struc, err := item.AsStructValue(); err == nil {
			data = struc.Data
		} else {
			return FAULT, errors.ERR_BAD_TYPE
		}

		for i, j := 0, len(data)-1; i < j; i, j = i+1, j-1 {
			data[i], data[j] = data[j], data[i]
		}
	case REMOVE:
		item, index, err := self.EvalStack.PopPair()
		if err != nil {
			return FAULT, err
		}
		switch item.GetType() {
		case types.MapType:
			value, err := item.AsMapValue()
			if err != nil {
				return FAULT, err
			}
			err = value.Remove(index)
			if err != nil {
				return FAULT, err
			}
		case types.ArrayType:
			value, err := item.AsArrayValue()
			if err != nil {
				return FAULT, err
			}
			i, err := index.AsInt64()
			if err != nil {
				return FAULT, err
			}
			err = value.RemoveAt(i)
			if err != nil {
				return FAULT, err
			}
		default:
			return FAULT, fmt.Errorf("[REMOVE] not support datatype")
		}
	case HASKEY:
		item, key, err := self.EvalStack.PopPair()
		if err != nil {
			return FAULT, err
		}
		mapValue, err := item.AsMapValue()
		if err != nil {
			return FAULT, err
		}
		_, ok, err := mapValue.Get(key)
		if err != nil {
			return FAULT, err
		}
		err = self.EvalStack.Push(types.VmValueFromBool(ok))
		if err != nil {
			return FAULT, err
		}
	case KEYS:
		item, err := self.EvalStack.Pop()
		if err != nil {
			return FAULT, err
		}
		mapValue, err := item.AsMapValue()
		if err != nil {
			return FAULT, err
		}
		keys := mapValue.GetMapSortedKey()
		arr := types.NewArrayValue()
		for _, v := range keys {
			err = arr.Append(v)
			if err != nil {
				return FAULT, err
			}
		}
		err = self.EvalStack.Push(types.VmValueFromArrayVal(arr))
		if err != nil {
			return FAULT, err
		}
	case VALUES:
		item, err := self.EvalStack.Pop()
		if err != nil {
			return FAULT, err
		}
		mapVal, err := item.AsMapValue()
		if err != nil {
			return FAULT, err
		}
		vals, err := mapVal.GetValues()
		arr := types.NewArrayValue()
		for _, v := range vals {
			err := arr.Append(v)
			if err != nil {
				return FAULT, err
			}
		}
		err = self.EvalStack.Push(types.VmValueFromArrayVal(arr))
		if err != nil {
			return FAULT, err
		}
	case THROW:
		return FAULT, nil
	case THROWIFNOT:
		val, err := self.EvalStack.PopAsBool()
		if err != nil {
			return FAULT, err
		}
		if !val {
			return FAULT, nil
		}
	default:
		return FAULT, errors.ERR_NOT_SUPPORT_OPCODE
	}

	return NONE, nil
}
```