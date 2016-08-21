Synopsis
========

    Usage: mkradmin <command> [<args>]
       or: mkradmin <command> --help

    Perform MakerDAO admin actions from the comfort of your command line.

    Commands:

       confirm       confirm proposed multisig action
       ls            list proposed multisig actions
       propose       propose new multisig action
       trigger       trigger confirmed multisig action

Examples
========

    ~$ mkradmin ls
     ACTION  CONFIRMATIONS      EXPIRATION  STATUS
         15   0/6 (need 4)        8 h left  Unconfirmed
         16   0/6 (need 4)        9 h left  Unconfirmed

    ~$ mkradmin propose @feedbase "claim()"
    Proposing multisig action...
      receiver   0x5927c5cc723c4486f93bf90bad3be8831139499e
      calldata   0x4e71d92d
    seth-send: 0x307b667c434794c234b7c463b26827bdceb9c838fdb306f3f4398edefa5b1310
    seth-send: Waiting for transaction receipt.........................
    seth-send: Transaction included in block 1519991.
    seth-send: note: return value may be inaccurate (see `seth send --help')
    Successfully proposed action 17.

    ~$ mkradmin ls
     ACTION  CONFIRMATIONS      EXPIRATION  STATUS
         15   0/6 (need 4)        8 h left  Unconfirmed
         16   0/6 (need 4)        9 h left  Unconfirmed
         17   0/6 (need 4)       23 h left  Unconfirmed

    ~$ mkradmin confirm 17
    Confirming action 17...
    seth-send: 0x72fc6bf7c5135645a0fa298aa3ae01e072a82eabfddc8e3fbcdca72d0007d94b
    seth-send: Waiting for transaction receipt...............
    seth-send: Transaction included in block 1520018.
    seth-send: note: return value may be inaccurate (see `seth send --help')
    0x

    ~$ mkradmin ls
     ACTION  CONFIRMATIONS      EXPIRATION  STATUS
         15   0/6 (need 4)        8 h left  Unconfirmed
         16   0/6 (need 4)        9 h left  Unconfirmed
         17   1/6 (need 4)       23 h left  Unconfirmed

    ~$ mkradmin trigger 17
    mkradmin-trigger: error: action not confirmed: 17

    ~$ mkradmin action 17
    confirmations   1
    confirmed       false
    expiration      1471876934
    expired         false
    triggered       false
    status          Unconfirmed
