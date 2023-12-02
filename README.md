# AlfaHack_bestrepository
Репозиторий для второго этапа хакатона от Альфа банка
Мы проделали следующий препроцессинг:
Выбросили признаки 'city', 'index_city_code', 'branch_code', 'cnt_days_cred_f_oper_1m', 'cnt_a_oper_1m', 'cnt_a_oper_3m', 'cnt_days_cred_g_oper_1m', 'cnt_deb_d_oper_1m', 'cnt_days_cred_g_oper_3m';
Заполнили Nan значения нулями в признаках 'max_end_plan_non_fin_deals','max_start_fin_deals', 'max_start_non_fin_deals', 'min_end_fact_fin_deals', 'min_start_fin_deals', 'min_start_non_fin_deals', 'max_founderpres', 'min_founderpres', 'max_end_fact_fin_deals', 'min_end_plan_non_fin_deals';
В признак rko_start_months убрали значения -999;
Проанализировали признаки channel_code, cities_types и убрали значения не несущие полезной для модели информации;
Признаки по месяцам преобразовали так чтобы не было смещения в распределении.
Две отдельных модели LGBMClassifier для предсказания target_1 и target_2 затем получение итогового предсказание с помощью невыпуклой комбинации этих двух предсказаний. (target_1 + target_2 -(target_1*target_2))
Гипперпараметры моделей:
для target_1: boosting_type = 'gbdt', max_depth=12, n_estimators=700, learning_rate=0.0645, reg_alpha=0.0328, reg_lambda=0.0984.
Для target_2: boosting_type = 'gbdt', n_estimators = 900,  max_depth = 12 , learning_rate = 0.0401,  reg_alpha = 0.0817,  reg_lambda = 0.086.
Подбор гиперпараметров был проведен с помощью optuna а также собственноручно собранного random search.
