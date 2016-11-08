# skb_2b: Фамилия И.О.

Решение в routes/index.js:

var express = require('express');
var router = express.Router();
var url = require('url');

/* GET home page. */
router.get('/', function(req, res, next) {
  let fiores = '';
  try {
    let fiostr = url.parse(req.url, true).query.fullname;
    if (fiostr) {
      let fioArr = fiostr.split(' ');
      switch (fioArr.length) {
        case 3:
          fiores = fioArr[2] + ' ' + fioArr[0].substr(0, 1) + '. ' + fioArr[1].substr(0, 1) + '.';
          break;
        case 2:
          fiores = fioArr[1] + ' ' + fioArr[0].substr(0, 1) + '.';
          break;
        case 1:
          fiores = fioArr[0];
          break;
        default:
          fiores = 'Invalid fullname';
      }
    } else {
      fiores = 'Invalid fullname';
    }
  } catch (e) {
    fiores = 'Invalid fullname';
  }
  res.render('index', { fio:  fiores});
});

module.exports = router;

