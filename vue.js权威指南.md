# Vue.jsȨ��ָ��

## Ԥ��Vue.js

### Vue.js��ʲô
1. ����
1. ���ݰ�
1. ָ��
1. �����

1. ��Ⱦһ�����ݣ�����ͨ����*��ʵ��

### ���ʽ
Mustache��ǩҲ���ձ��ʽ��ʽ��ֵ

{{lat/100}}
{{true?1:0}}
{{example.split(",")}}

vue.js�����ڱ��ʽ����ӹ�����(������һ������)

{{example|toUpperCase}}
{{example|filterA|filterB}}
{{example|filter a b}}

### ָ��
ָ���Ǵ�������V-ǰ׺���������ԣ���ֵ�޶�Ϊ�󶨱��ʽ��Ҳ����js���ʽ�͹�������ָ��������Ǳ��ʽ��ֵ�����仯ʱ������仯Ҳ��ӳ��dom�ϣ��������£�
<div v-if='show'>DDFE</div>
��showΪtrueʱ��չʾDDFE������չʾ

### �ָ���
vue.js�е����ݰ󶨵��﷨�����Ϊ�����õġ������ϰ��Mustache�����﷨��������Լ����á�
������vue.config�����ð󶨵��﷨��
vue.config��һ�����󣬰���������vue������ȫ�����ã�������vueʵ����ǰ�޸����е����ԡ�

## ָ��

### �ڲ�ָ��
1. v-show
1. v-else
1. v-model
1. v-repeat
1. v-for
1. v-text
1. v-el
1. v-html
1. v-on
1. v-bind
1. v-ref
1. v-pre
1. v-cloak
1. v-if

#### v-if
���ݱ��ʽ��ֵ��DOM�����ɻ��Ƴ�һ��Ԫ�أ��������Ϊfalse,��ô��Ӧ��Ԫ�ؾͻ��DOM���Ƴ������򣬶�ӦԪ�ص�һ����¡�����²���DOM��

#### v-show
���ݱ��ʽ��ֵ����ʾ������HTMLԪ�أ���Ϊfalse��Ԫ���϶���һ��������ʽstyle='display:none'
>>v-show��֧��<template>�﷨