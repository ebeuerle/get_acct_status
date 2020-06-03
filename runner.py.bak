import lib
import json

class AccountStatus():
    def __init__(self):
        self.config = lib.ConfigHelper()
        self.csv_writer = lib.CsvWriter()
        self.rl_sess = lib.RLSession(self.config.rl_user,self.config.rl_pass,self.config.rl_cust,self.config.rl_api_base)
        self.output = [["AccountNumber", "Name", "Status", "subComponents_name", "subComponents_message", "subComponents_remediation"]]

    def build(self):
        self.url = "https://" + self.config.rl_api_base + "/cloud/name?onlyActive=true"
        self.rl_sess.authenticate_client()
        response = self.rl_sess.client.get(self.url)
        #write out the top of csv to file
        self.csv_writer.write(self.output)
        json_response = response.json()
        for cloudacctdetails in json_response:
            self.status_url = "https://" + self.config.rl_api_base + "/account/%s/config/status" % cloudacctdetails["id"]
            status_resp = self.rl_sess.client.get(self.status_url)
            json_status_resp = status_resp.json()
            for csp_status in json_status_resp:
                if csp_status['status'] == "error":
                    data = [cloudacctdetails['id'],csp_status['name'],csp_status['status'],csp_status['message'],csp_status['remediation']]
                    self.csv_writer.append([data])
                else:
                    for sub in csp_status['subComponents']:
                        data = [cloudacctdetails['id'],csp_status['name'],csp_status['status'],sub['name'],sub['message'],sub['remediation']]
                #encoded_data = [x.encode('utf-8') for x in data]
                        self.csv_writer.append([data])

    def run(self):
        self.build()

def main():
    rl_acct_status = AccountStatus()
    rl_acct_status.run()


if __name__ == "__main__":
    main()
